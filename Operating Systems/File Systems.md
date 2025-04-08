So we have persistent data, but as we've covered, it's unwise to operate with it directly through hardware. How can we abstract that data and what interface do operating systems provide for files?

## Abstractions
First, the basics. A **file** is a persistent linear array of bytes on disk. Every file will have a unique name --- a **low-level** number, or **inode** number. We want to read, write, or **seek** (read from an offset position in the file) these files. Most of the time, `seek` is encoded into `read`. However, we don't want to specify the inode number for each file. That's way too difficult for us humans to remember. 
We'll introduce an item for the organization of files: **directories**. These are mappings between names and inode numbers. Each file in the directory can be considered a name/inode number pair (name is an abstraction for humans to remember files). 
These directories can be thought of as a tree. For example, the root in Unix is **/**, and it includes directories such as **bin**, **usr**, etc.. We can **mount** a file system by setting it as a child to a leaf on the tree. 
This proposes a problem. To find a nested file, we need to read the inode number of each directory parent. This could be expensive. Thus, we introduce another abstraction: **file descriptors**. Every process will have a file descriptor hash table that includes all open files. The first few entries are typically `stdin/stdout` and other common standard files. The others are hashes to files, which include the offset, inode, and reference. We'll modify `open` so it returns the file descriptor, and `read` and `write` so they use the file descriptor. Also, `seek` is back! It now updates the per-process offset of the file. 

We have a few abstractions; let's figure out how they change our OS methods. 
`fork` is now going to increase the reference count of each open file's file descriptor. `close` decrements the reference count, and we flush the file's data to the disk. 
Unfortunately, writers have high latency. This means it's more effective to cache data in memory and write it larger, less frequent chunks. This also means that applications may need to instruct the OS to write certain data immediately (avoiding data loss after a crash). This is the point of the `fsync` command. 

Luckily for us, renaming a file is simple. We can update the directory data with a new mapping, but the inode doesn't change, so processes don't need their file descriptor tables updated. 

Finally, we need to consider what happens when we delete a file. When we use a function like `rm`, we typically **unlink** a file, not fully removing it. This also means we can create more links to a file with `ln`. This creates what looks like a different file with a different name, but checking the name with `stat` will reveal the same inode number. This increases the reference count. Also, having two links to the same file doesn't change permissions; the page directory stores permissions. 
Another type of link is the **softlink**, with `ln -s`. Soft links do not increase reference count because they refer to the other file link, not the file itself. 

After this, we have the basics to start the greatest abstraction of all: the **file system (FS)**. 

## Very Simple File System (VSFS)
Your files are stored in a very large array. Part of the array is reserved for data and part is reserved for inodes (the metadata). The elements of the array are typically 4KB blocks to match page sizes for convenience. 
There's one inode per file and it stores the size, timestamps, permissions, links, and type (file or directory). 
Then, there's **data blocks**. These are the files with file data or directories with hashes that map names to inode numbers. One file can use multiple data blocks. 
But how does a program know which regions are which before iterating through them? The elements before both the inode and data regions are the **ibit and dbit masks**. The ibits track the allocated inode blocks and the dbits track the allocated data blocks. 
NOTE: if a file is empty, it doesn't set a dbit for the file; it waits for the memory to be allocated and used first. 
NOTE: the bitmaps are only for allocations, so reads don't need to access the bitmap. 
Bu how does the program know where those bit maps are? We create one more block: the **superblock**. It contains the ibit location, dbit location, inode region, data region, and "magic number" (which may or may not be used depending on the FS). 

Ok, we have files in an array. However, the array is really long, and files themselves are virtual arrays of bytes. How do we optimally organize file data on a disk? Moreover, how can we map the virtual array of bytes to the physical resource (disk or SSD)?
There are a few problems to think about. What are they?
What about **fragmentation**? Internal and external? 
What about the seek cost of the files?
What about metadata storage?

### Contiguous Allocation
Like the array idea. Seek cost is low --- it's just indexes in an array. The metadata is pretty small as well. However, external fragmentation is horrible. Finally, if we want to grow a file, then what? Do we have to iterate over the entire array? This idea is a little naive. 

#### Extent Allocation
We make a new list. Keep in this list the *addresses* and *lengths* of files. External fragmentation is better, but it relies on a static number of extents. 

### Fixed-Size Data Blocks
If the previous idea was similar to the naive heap approach to memory, this is akin to the page table approach. 

#### Linked List
We make a linked list of of inodes and data. This has extremely poor seek time but no external fragmentation. It does have internal fragmentation. Let's throw it out. 

#### File Allocation Table (FAT)
Keep the linked list in a separate table. The table includes block indices and the next block indices to that block. We can read this whole table and cache it for quick random access. 

#### Direct Reference
Introduce the **index block**, a pointer to data blocks. Random access is good and sequential access is fine, although it requires an extra read. 
The index block itself is a bit of a bottleneck, but we can alleviate some of those inefficiencies through hierarchical indexing. The inode is now a tree-like structure with references to data blocks (small number, maybe 10), then indirect blocks off of those blocks (larger, maybe 1024), and onwards as the tree grows. 

Here's an example.
You open `/foo/bar`. Assuming the superblock is cached, you have to access the root inode, root data, foo inode, foo data, and bar inode. 
Question: Do you have to access the bar data?
Answer: No. You are just opening the file, not reading just yet. 

Here's another example. 
You *create* `/foo/bar`. Assuming the superblock is cached, you access the root inode, root data, foo inode, and foo data. 
Question: What do the next two steps happen to?
Answer: The *inode bitmap*.
Steps 5 and 6 are to read the inode bit map for the next available data block and to write to the inode bit map to make space for bar. 
Step 7 is to write to the foo data block. Remember, bar is in the foo directory. 
Steps 8 and 9 are to read and write to the bar inode. Finally, step 10 is to write to the foo inode. This is done last for error protection; if there was a crash before step 10, we don't want the foo directory to include a file that doesn't exist. 

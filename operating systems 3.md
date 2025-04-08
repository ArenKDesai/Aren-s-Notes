# File Systems

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
Question: What do the next two steps happen to
Answer: Th
Steps 5 and 6 are to read the inode bit map for the next available data block and to write to the inode bit map to make space for bar. 
Step 7 is to write to the foo data block. Remember how we 

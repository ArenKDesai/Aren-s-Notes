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


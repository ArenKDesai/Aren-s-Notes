# File Systems

## Very Simple File System (VSFS)
Your files are stored in a very large array. Part of the array is reserved for data and part is reserved for inodes (the metadata). The elements of the array are typically 4KB blocks to match page sizes for convenience. 
There's one inode per file and it stores the size, timestamps, permissions, links, and type (file or directory). 
Then, there's **data blocks**. These are the files with file data or directories with hashes that map names to inode numbers. One file can use multiple data blocks. 
But how does a program know which regions are which before iterating through them? The elements before both the inode and data regions are the **ibit and dbit masks**. The ibits track the allocated inode blocks and the dbits track the allocated data blocks. 
Bu how does the program know where those bit maps are? We create one more block: the **superblock**. It contains the ibit location, dbit l
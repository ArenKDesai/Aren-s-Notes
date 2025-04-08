# File Systems

## Very Simple File System (VSFS)
Your files are stored in a very large array. Part of the array is reserved for data and part is reserved for inodes (the metadata). The elements of the array are typically 4KB blocks to match page sizes for convenience. 
There's one inode per file
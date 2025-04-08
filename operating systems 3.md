# File Systems

## Very Simple File System (VSFS)
Your files are stored in a very large array. Part of the array is reserved for data and part is reserved for inodes (the metadata). The elements of the array are typically 4KB blocks to match page sizes for convenience. 
There's one inode per file and it stores the size, timestamps, permissions, links, and type (file or directory). 
Then, there's **data blocks**. These are the files with file data or directories with hashes that map names to inode numbers. 
But 
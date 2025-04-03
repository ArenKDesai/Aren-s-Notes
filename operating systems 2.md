So we have persistent data, but as we've covered, it's unwise to operate with it directly through hardware. How can we abstract that data and what interface do operating systems provide for files?

## Abstractions
First, the basics. A **file** is a persistent linear array of bytes on disk. Every file will have a unique name --- a **low-level** number, or **inode** number. We want to read, write, or **seek** (read from an offset position in the file) these files. Most of the time, `seek` is encoded into `read`. However, we don't want to specify the inode number for each file. That's way too difficult for us humans to remember. 
We'll introduce an item for the organization of files: **directories**. These are mappings between names and inode numbers. Each file in the directory can be considered a name/inode number pair (name is an abstraction )
These directories can be thought of as a tree. For example, the root in Unix is **/**, and it includes directories such as **bin**, **usr**, etc.. We can **mount** a file system by setting it as a child to a leaf on the tree. 

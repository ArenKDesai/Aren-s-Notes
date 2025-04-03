So we have persistent data, but as we've covered, it's unwise to operate with it directly through hardware. How can we abstract that data and what interface do operating systems provide for files?

## Abstractions
First, the basics. A **file** is a persistent linear array of bytes on disk. Every file will have a unique name --- a **low-level** number, or **inode** number. 
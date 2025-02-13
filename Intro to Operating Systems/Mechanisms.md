#UWMadison 

The OS needs a place to store portions of address spaces that currently aren't in great demand. This is naturally slower than memory, but has more capacity. Typically, this is the **hard disk drive (HDD)**. 

## Swap Space
The swap space is used to move pages in and out of memory. The OS needs to remember the **disk address** of any given page to do this. 

If a VPN is requested and not found in the TLB ([[Paging]]), the hardware needs to find the **page table entry (PTE)** of the page. The **present bit** tells if a page is in memory -  1 for present, 0 for not. 
A **page fault** is when a program tries to access a part of the virtual address space that the OS has swapped out to the disk. This invokes the **page-fault handler**. 

While the I/O is in flight, the currently running process will be in a **blocked** state ([[Processes]]). This includes page faults, so if a page fault is currently being thrown, the OS can use that time to service another process. 
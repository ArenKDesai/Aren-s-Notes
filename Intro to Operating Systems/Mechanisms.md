#UWMadison 

The OS needs a place to store portions of address spaces that currently aren't in great demand. This is naturally slower than memory, but has more capacity. Typically, this is the **hard disk drive (HDD)**. 

## Swap Space
The swap space is used to move pages in and out of memory. The OS needs to remember the **disk address** of any given page to do this. 

If a VPN is requested and not found in the TLB ([[Paging]]), the hardware needs to find the **page table entry (PTE)** of the page. The **present bit** tells if a page is in memory -  1 for present, 0 for not. 
A **page fault** is when a program tries to access a part of the virtual address space that the OS has swapped out to the disk. This invokes the **page-fault handler**. 

While the I/O is in flight, the currently running process will be in a **blocked** state ([[Processes]]). This includes page faults, so if a page fault is currently being thrown, the OS can use that time to service another process. 

## Page Replacement Polices
If memory is full, the OS may need to **page out** one or more pages so it can replace it with a different page. This requires a policy for page replacements. 
Typically, the OS keeps a **high watermark** and **low watermark**. These act as bounds for the number of free pages that can be used. The thread that manages these bounds is called the **swap daemon** or **page daemon**. 

## Page Caching
Our main memory can be viewed as a cache for virtual memory pages in the system. We can calculate a useful metric, the **average memory access time (AMAT)**, for a program as the following:
$AMAT=T_M+(P_{miss}*T_D)$
$T_M$ repres
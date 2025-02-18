#UWMadison #OperatingSystems #CS537

The OS needs a place to store portions of address spaces that currently aren't in great demand. This is naturally slower than memory, but has more capacity. Typically, this is the **hard disk drive (HDD)**. 

## Swap Space
The swap space is used to move pages in and out of memory. The OS needs to remember the **disk address** of any given page to do this. 

If a VPN is requested and not found in the TLB ([[Paging]]), the hardware needs to find the **page table entry (PTE)** of the page. The **present bit** tells if a page is in memory -  1 for present, 0 for not. 
A **page fault** is when a program tries to access a part of the virtual address space that the OS has swapped out to the disk. This invokes the **page-fault handler**. 

While the I/O is in flight, the currently running process will be in a **blocked** state ([[Processes]]). This includes page faults, so if a page fault is currently being thrown, the OS can use that time to service another process. 

This works due to **locality of reference**, or the idea that **spatial** and **temporal** locality can be manipulated to optimize memory access. 

### Swapping Polices
Page faults are slow, sometimes requiring 1,000,000x times the cost of a normal instruction. This means decisions must be made on how to handle a page fault. These two decisions are:
1. When should a page on disk be brought into memory?
2. Which resident page in memory should be moved out to disk?

The first policy for the first question is **demand paging**: Only load in a page when a page fault occurs. This throws a page fault for every new page, so the cost of this one is huge. 
The second policy is **prepaging**: loading the page before it's referenced. 

### Virtual Memory Area
The table of information on allocated memory with **permissions**, **present bits**, and **valid bits**. The hardware only cares about permissions and the present bit; the OS cares about the valid bit. When the page is on disk, the PPN is the physical location on disk; when the page is in memory, the PPN is the location on the page table. 
When looking for a page, the hardware checks the TLB first. If there's a hit, the page is in physical memory. If there's a miss, the present bit is checked. If the present bit is not set, a **page fault** is thrown and the OS is called through a trap.** 

## Page Replacement Polices
If memory is full, the OS may need to **page out** one or more pages so it can replace it with a different page. This requires a policy for page replacements. 
Typically, the OS keeps a **high watermark** and **low watermark**. These act as bounds for the number of free pages that can be used. The thread that manages these bounds is called the **swap daemon** or **page daemon**. 

The optimal policy has been shown to be **Furthest in the Future** ([[Greedy]]), although it is difficult to implement. 

### Page Caching
Our main memory can be viewed as a cache for virtual memory pages in the system. We can calculate a useful metric, the **average memory access time (AMAT)**, for a program as the following:
$AMAT=T_M+(P_{miss}*T_D)$
$T_M$ represents the cost of accessing memory, $T_D$ is the cost of accessing disk, and $P_{miss}$ is the probability of a cache miss. The cost of disk access usually makes even a single cache miss very significant. 
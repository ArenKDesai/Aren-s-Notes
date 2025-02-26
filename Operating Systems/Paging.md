#UWMadison #CS537 #OperatingSystems 

Allocating memory in the [[Address Space]] is usually done with a heap that can be allocated to processes, but this causes problems, such as external fragmentation. Paging solves this by allocating memory in fixed-size **pages**, similar to an array of finite-sized memory pieces. 
These pages can be pretty convenient since the OS doesn't have to worry about how the memory structures (stack, heap, etc) grow, along with other useful abstractions. 
Pages are stored in page frames.

## Page Table
Page locations and availability are stored in the **page table**, a **per-process** data structure that stores address translations so the OS can know where the physical memory for each page resides. The details of the pages are kept in a **page table entry (PTE)**. Since each process has its own page table and PTE, we can give different processes different permissions. 
The new equation for virtual address translation is a little more complicated. The first (leftmost) bits are used as the **virtual page number (VPN)**, and the rest is the offset. 
Imagine we have 16 byte pages in a 64 byte address space. We'd have $\frac{64}{16}=4$ pages, of which we could cover the VPNs for with $4=2^x$, $\log(4)=x\log(2)$, $x=2$ bits. 

Now imagine we have a 20-bit VPN. This would be $2^{20}$ address translations the OS would have to manage for *every process*. 

The typical page size is 4kb, so we'd have 12 bits of the address. The page table would need to be 4MiB to hold all those processes. With 64-bit processors, we'd need 36 exa-bytes. 
However, most address space is sparse (has holes mapped to nothing). Software-managed page tables were tested, but they were too slow. This was fixed with multilevel page tables. This allows page table to be allocated non-contiguously. 
To calculate address, take the first hex, find the page of PT with it, find the second hex (inner address), find the address with it, add offset (rest of hex). 

### Page Table Organization
In all forms of a page table, a **valid bit** is used to indicate whether a translation is valid. This is the origin of a **page fault**. 
Sometimes, there's also a **protection bit** that indicates the page permissions (read, write, execute). 
A **present bit** indicates whether the page is in physical memory or on disk. 
It's also common to have a **dirty bit** that indicates whether a page has been modified since it was brought into memory. 
A **reference bit** is used to track whether a page has been accessed. 

The easiest form of a page table to implement is the **linear page table**. This is just an array of pages. The VPN acts as an index into the page table. 

In order to find stored data, the system must:
1. Fetch the PTE that carries the desired data from the process's page table
2. Translate the address from the PTE
3. Load the data from the address into physical memory. 
However, the hardware must first find the page table for the currently running process. Sometimes, the physical address of the starting location is stored in a **page table base register**. Then, these equations are ran:
$VPN = (Virtual\ Address\ \&\ VPN\ Mask) >> Shift$
$PTE\ Address = Page\ Table\ Base\ Register+(VPN\cdot sizeof(PTE))$
We can find the PTE from the PTE Address, and the hardware can proceed to extract the data from memory and put it in register $eax$. 

### Working Set
We've set up processes to have virtual memory, but how do we decide how much memory a process needs? 
We define the working set for a process at time $t$ as $W(D,t)$, where $D$ is a window of time and $W$ ends up being an approximation of the program's locality. We can give a process an amount of memory that is a function of the amount of pages it has used in the last time step (and if it's the first time the program has run, guess). 
This also works as a function of page faults. More page faults means we need more memory, and vice versa. 
All information related to the working set is stored in the PCB. 

If you take the curve relating the number of page frames to the page fault rate, you can find a point of inflection that acts as that approximation for the correct working set size. 

## Translation-Lookaside Buffer (TLB)
We want to speed up address translation, so we use a **translation-lookaside buffer (TLB)**. This is a part of the **memory-management unit (MMU)**, and it caches address translations. The TLB acts like a typical cache that keeps high-frequency address translations in on-chip memory. 

The algorithm works as follows:
1. Get VPN from virtual address
2. Check if TLB has the translation into physical address for this VPN
3. If the TLB does have the translation, great! If not, we handle a TLB miss. 

Old architectures had **hardware-managed TLBs**, like Intel x86, with a fixed multi-level page where TLB misses would manually walk through the page for the correct address translation. Modern architectures are either **reduced-instruction set computers (RISC)** (less common) or **complex-instruction set computers (CISC)** (more common) with a software-managed TLB. On a miss, the hardware raises an exception, which pauses the current instruction stream, raises the privilege level to kernel mode, and jumps to a trap handler. 
The OS must take care to never end up in a TLB-miss loop. Some solutions include keeping TLB miss handlers in unmapped physical memory, or reserving some memory for the TLB-miss handler address translation permanently. 

A TLB typically has 32, 64, or 128 entries, and be a **fully-associative** TLB. This means that any given translation could be anywhere in the TLB - no restrictions or special cases. A TLB entry of this nature will typically consist of a VPN, a PFN (physical location address), and some bits used for bookkeeping. For example, the TLB has a valid bit that states whether an entry has a valid translation. Sometimes there's also protection bits, which include information such as "read, write, execute". 

Context switches provide a challenge, since we don't want one process to use another's addresses. One solution is to flush the TLB. Another solution is to provide an **address space identifier (ASID)** to ensure correct address space usage (similar to a PID). 

The TLB typically evicts pages either using the policies Least Recently Used (LRU) or random eviction ([[Caches]]). 

The TLB has a reach that states how much memory can be accessed before a miss is registered. For Intel, this is typically separated into L1, L2, etc. L1 has 64 entries and 1 cycle, L2 has 1536 entries and 7 cycles, etc. Since the **TLB reach = num entries x page size**, L1 isi 4kb x 64 = 256kb per core. 

The speed at which the TLB operates can vary wildly per operating system, and sometimes may even consume 40%-80% of total computing time. It's also variable whether the OS or the hardware handles TLB misses. 

## Page Sizes
Each process needs a page table with a page every page it needs to access, which could add up to abominable amount of memory used on page tables. 

*Idea 1: Large Pages*
Having larger pages would allow us to store more memory the process requires without the need for overhead. However, these large pages can easily lead to **internal fragmentation** if we have a lot of processes that don't need much memory. 

*Idea 2: Small Pages*
Extreme amounts of external fragmentation due to invalid spaces. 

***Idea 3: Multiple Page Tables***
We make a page table per logical segment of the process's memory. The base and bounds registers stay on the MMU, but the base register now points towards the physical address of the page table. The bounds register points to the end of the page table (number of pages). 

In this format, under a TLB miss, we have three new equations. The first is to calculate the **segment number**, which we find from the virtual address, the segment mask, and the segment number shift:
$SN=(Virtual\ Address\&Segment\ Mask)>>Segment\ Number\ Shift$.
The virtual page number can be calculate from the virtual address, VPN mask, and VPN shift:
$VPN=(Virtual\ Address\&Virtual\ Page\ Number\ Mask)>>Virtual\ Page\ Number\ Shift$.
Finally, we can calculate the address of the page table entry from indexing the base register with the segment number and adding the VPN multiplied by the size of the page table entry:
$Address\ of\ Page\ Table\ Entry=Base[Segment\ Number]+(Virtual\ Page\ Number\cdot sizeof(Page\ Table\ Entry))$

### Multi-Level Page Table
The Multi-Level Page Table (MLPT) utilizes a data structure more similar to a tree than an array. 
We track all pages with a **page directory**. The base register points to the page directory, and the page directory contains **page directory entries (PDEs)**. These PDEs contain a valid bit and a **page frame number**, and point to page tables. The valid bit states whether at least one of the pages in the page table is valid. 
This tree-like format (called a **level of indirection**) allows us to use any point of physical memory for pages. 

However, on a TLB miss, two loads from memory will be required. This is a **time-space trade-off**. 

With a VPN / offset bitarray, the first four (leftmost) bits are used for the page directory

### Huge Pages
If we have a much larger sized page, we need to allocate more bits to the offset. The 18 bits that are usually allocated to the page directory and page table are used for the offset, so every level of the page table will have a bit that states if the pointer points to the next level or the larger page table entry. 
One way to request these large pages is to request them with **mmap(MAP_HUGE)**. This will allocate a huge page or fail. The other method is by using **transparent huge pages (THP)**, which automatically uses huge pages for >2MB allocations. This means creating large pages is slow and it may not be necessary. However, this keeps control in the hands of the OS, which is often more knowledgeable than the programmer. 
ex:
```C
double sum = 0.0;
double a[1024*1024];
// randomly access all items of array
```
The above code is 8MB / 2MB = 4 large pages, so we have $4/1024^2$ miss rate (~0%). 
If we used small pages, we'd have $2*1024$ small pages (8MB / 4kB), all of which are going to miss. 

### Copy-On-Write
When calling ```fork```, the OS can use **copy-on-write (COW)** to create a shared mapping of the parent pages in the child address space instead of copying the page table. The child will have reduced permissions, so a child doing a write will cause a protection fault, which will copy the page and resume the child process. This protection fault will trap for every page that is written to, so if the child process tries to write to every page, this would actually be slower. 

### Thrashing
If you run out of memory, you end up trashing pages directly after bringing them into memory. This is called thrashing, where most of your time is spent in page faults. The solution is often to start randomly killing processes using the most memory. 
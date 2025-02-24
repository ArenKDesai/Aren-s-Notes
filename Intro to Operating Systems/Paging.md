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
The easiest form of a page table to implement is the **linear page table**. This is just an array of pages. The VPN acts as an index into the page table. 

In all forms of a page table, a **valid bit** is used to indicate whether a translation is valid. This bit being 0 cau

## Translation-Lookaside Buffer (TLB)
We want to speed up address translation, so we use a **translation-lookaside buffer (TLB)**. This is a part of the **memory-management unit (MMU)**, and it caches address translations. The TLB acts like a typical cache that keeps high-frequency address translations in on-chip memory. 

Old architectures had **hardware-managed TLBs**, like Intel x86, with a fixed multi-level page where TLB misses would manually walk through the page for the correct address translation. Modern architectures are **reduced-instruction set computers (RISC)** with a software-managed TLB. On a miss, the hardware raises an exception, which pauses the current instruction stream, raises the privilege level to kernel mode, and jumps to a trap handler. 
The OS must take care to never end up in a TLB-miss loop. Some solutions include keeping TLB miss handlers in unmapped physical memory, or reserving some memory for the TLB-miss handler address translation permanently. 

The TLB has a valid bit that states whether an entry has a valid translation. Sometimes there's also protection bits, which include information such as "read, write, execute". 

Context switches provide a challenge, since we don't want one process to use another's addresses. One solution is to flush the TLB. Another solution is to provide an address space identifier (ASID) to ensure correct address space usage. 

The TLB has a reach that states how much memory can be accessed before a miss is registered. For Intel, this is typically separated into L1, L2, etc. L1 has 64 entries and 1 cycle, L2 has 1536 entries and 7 cycles, etc. Since the **TLB reach = num entries x page size**, L1 isi 4kb x 64 = 256kb per core. 

The speed at which the TLB operates can vary wildly per operating system, and sometimes may even consume 40%-80% of total computing time. It's also variable whether the OS or the hardware handles TLB misses. 

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
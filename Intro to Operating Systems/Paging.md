Paging transforms traditional memory allocation from a large buffer of memory to something more like an array of finite-sized elements. These are pages. 

Page locations and availability are stored in the **page table**. This stores **address translations** so the OS can know where the physical memory for each page resides. 

## Translation-Lookaside Buffer (TLB)
We want to speed up address translation, so we use a **translation-lookaside buffer (TLB)**. This is a part of the **memory-management unit (MMU)**, and it caches address translations. The TLB acts like a typical cache that keeps high-frequency address translations in on-chip memory. 

Old architectures had **hardware-managed TLBs**, like Intel x86, with a fixed multi-level page where TLB misses would manually walk through the page for the correct address translation. Modern architectures are **reduced-instruction set computers (RISC)** with a software-managed TLB. On a miss, the hardware raises an exception, which pauses the current instruction stream, raises the privilege level to kernel mode, and jumps to a trap handler. 
The OS must take care to never end up in a TLB-miss loop. Some solutions include keeping TLB miss handlers in unmapped physical memory, or reserving some memory for the TLB-miss handler address translation permanently. 

The TLB has a valid bit that states whether an entry has a valid translation. Sometimes there's also protection bits, which include information such as "read, write, execute". 

Context switches provide a challenge, since we don't want one process to use another's addresses. One solution is to flush the TLB. Another solution is to provide an address space identifier (ASID) to ensure correct address space usage. 

The TLB has a reach that states how much memory can be accessed before a miss is registered. For Intel, this is typically separated into L1, L2, etc. L1 has 64 entries and 1 cycle, L2 has 1536 entries and 7 cycles, etc. Since the **TLB reach = num entries x page size**, L1 isi 4kb x 64 = 256kb per core. 

The speed at which the TLB operates can vary wildly per operating system, and sometimes may even consume 40%-80% of total computing time. It's also variable whether the OS or the hardware handles TLB misses. 

## Page Table
The typical page size is 4kb, so we'd have 12 bits of the address. The page table would need to be 4MiB to hold all those processes. With 64-bit processors, we'd need 36 exa-bytes. 
However, most address space is sparse (has holes mapped to nothing). Software-managed page tables were tested, but they were too slow. This was fixed with multilevel page tables. This allows page table to be allocated non-contiguously. 
To calculate address, take the first hex, find the page of PT with it, find the second hex (inner address), find the address with it, add offset (rest of hex). 

### Huge Pages
If we have a much larger sized page, we need to allocate more bits to the offset. The 18 bits that are usually allocated to the page directory and page table are used for the offset, so every level of the page table will have a bit that states if the pointer points to the next level or the larger page table entry. 
One way to request these large pages is to request them with **mmap(MAP_HUGE)**. This will allocate a huge page or fail. The other method is by using **transparent huge pages (THP)**, which automatically uses huge pages for >2MB allocations. This means creating large pages is slow and it may not be necessary. However, this keeps control in the hands of the OS, which is often more knowledgeable than the programmer. 
ex:
```C
double sum = 0.0;
double a[1024*1024];
// randomly access all items of array
```
The above code is 8MB / 2MB = 4 large pages, so we have $4/1024^2$ miss rate. 
If we used small pages, we'd have $2*1024$ small pages, all of which are going to miss. 
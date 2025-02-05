
## Translation-Lookaside Buffer (TLB)
We want to speed up address translation, so we use a **translation-lookaside buffer (TLB)**. This is a part of the **memory-management unit (MMU)**, and it caches address translations. The TLB acts like a typical cache that keeps high-frequency address translations in on-chip memory. 

Old architectures had **hardware-managed TLBs**, like Intel x86, with a fixed multi-level page where TLB misses would manually walk through the page for the correct address translation. Modern architectures are **reduced-instruction set computers (RISC)** with a software-managed TLB. On a miss, the hardware raises an exception, which pauses the current instruction stream, raises the privilege level to kernel mode, and jumps to a trap handler. 
The OS must take care to never end up in a TLB-miss loop. Some solutions include keeping TLB miss handlers in unmapped physical memory, or reserving some memory for the TLB-miss handler address translation permanently. 

The TLB has a valid bit that states whether an entry has a valid translation. Sometimes there's also protection bits, which include information such as "read, write, execute". 

Context switches provide a challenge, since we don't want one process to use another's addresses. One solution is to flush the TLB and
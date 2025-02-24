#CS537 #UWMadison #OperatingSystems 

Developer-made processes need to utilize a computer's memory in order to function. However, the physical locations of memory are hidden by the OS, so memory is virtualized ([[Virtualization]]). So how does the OS efficiently handle allowing processes to allocate virtual memory?

## Base and Bounds
The first idea is to take the process's memory and place it into physical memory like placing a peg into a hole. This idea allows the hardware to fully handle address translation, a notion known as **base and bounds**, or dynamic relocation. 
CPU needs two hardware registers: the **base register** and the **bounds register** (or limit register). Before runtime of the process, the OS sets the base register to the physical location of the memory of the process. This is a simple calculation:
$physical\ address = virtual\ address + base$. 
The bounds register is used to keep virtual address translations within reasonable bounds. This is helpful to avoid querying the hardware for the memory in an address that doesn't exist, which could cause serious problems. 
The part of the processor that handles address translations (and where the base and bounds registers are) is called the **memory management unit (MMU)**. 

When the OS hands off control to a process, it must save the base and bounds registers. It saves these register to the **process control block (PCB)**. 

## Segmentation
With just our operating system and the process stack/heap/code injected into physical memory, the current memory design looks like this:
![[basic_mem_hierarchy.png]]
There's a lot of lost space. Base and bounds on the full physical memory is wasteful, and also doesn't allow the OS to run programs larger than the full address space. 
The solution to this problem is **segmentation** on the address space. Each segment gets its own base/bounds pair. 
During address translation, instead of adding the base value to the virtual address, the hardware adds the base value to the offset of the segment. The first two bits of the virtual address is typically used to find the segment. 

Segmentation can either be **fine-grained** (large number of smaller segments) or **coarse-grained** (small number of large segments). 

To be able to share code (in the form of libraries), the hardware configures a **protection bit**. This is the common Read-Write-Execute permission bit indicator. 

### Stack
The stack acts a bit strangely in address translations into segments. The hardware always uses the top two bits of a virtual address to find the segment, but instead of using the offset directly, the hardware completes this calculation: $negative\ offset = offset - maximum\ segment\ size$. 

### Fragmentation
The memory in segments proposes a problem: a multitude of processes allocating memory in the address space can create a multitude of holes in-between processes. These holes aren't large enough to be used by anything, but are large enough to eat up memory. This is **external fragmentation**. 
The easiest fix for external fragmentation is to re-arrange memory allocation. However, this process is endlessly expensive, and not practical. 
Another idea is to keep a list of free memory spaces that algorithm can manage. Algorithms like **best-fit** (allocate memory with the space closest to the requested size), **worst-fit**, **first-fit**, etc. have all been prototyped, but extern
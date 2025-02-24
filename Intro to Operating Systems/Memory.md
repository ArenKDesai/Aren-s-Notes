Memory is the storage space that a program uses to store its functions, variables, etc. It exists both in the virtual space and physical, with the physical space being slower but having far greater quantity of storage. Memory exists in the [[Memory Hierarchy]], which organizes memory in a way that keeps frequently accessed memory in faster partitions closer to the processor. 

Programs (like C programs) allocate memory either **automatically (stack)** or **dynamically (heap)**, or manually by the developer. C allows for developers to call the ```malloc``` function (and other related functions like ```realloc``` and ```calloc```). 

**Multiprogramming** is when multiple programs are ready to run at the same time. The CPU can only actually run one process, so virtualization ([[OS Basics]]) is used to allow for multiprogramming. An address space is used to virtualize memory for a process. 

An address space typically consists of the following (top-down):
1. Program Code
2. Heap - for users to dynamically allocate memory. Grows down. 
3. Stack - memory space for the process's details. Grows up. 

Virtual memory wants to be **transparent** --- invisible, not openly available --- as well as efficient and secure. 

## Address Translation
The hardware transforms virtual addresses to physical addresses. This is done with dynamic relocation, where any privlidged process can directly write to physical addresses, but unprivlidged process write to a logical address, which is added with a base register to find a physical address. 
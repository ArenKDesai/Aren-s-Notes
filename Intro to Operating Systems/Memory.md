**Multiprogramming** is when multiple programs are ready to run at the same time. The CPU can only actually run one process, so virtualization ([[OS Basics]]) is used to allow for multiprogramming. An address space is used to virtualize memory for a process. 

An address space typically consists of the following (top-down):
1. Program Code
2. Heap - for users to dynamically allocate memory. Grows down. 
3. Stack - memory space for the process's details. Grows up. 

Virtual memory wants to be **transparent** --- invisible, not openly available --- as well as efficient and secure. 

## Address Translation
The hardware transforms virtual addresses to physical addresses. This is done with dynamic relocation, where any privlidged proces
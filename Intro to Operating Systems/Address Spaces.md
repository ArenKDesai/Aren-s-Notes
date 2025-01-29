**Multiprogramming** is when multiple programs are ready to run at the same time. The CPU can only actually run one process, so virtualization ([[OS Basics]]) is used to allow for multiprogramming. An address space is used to virtualize memory for a process. 

An address space typically consists of the following (top-down):
1. Program Code
2. Heap - for users to dynamically allocate memory. Grows down. 
3. Stack - 
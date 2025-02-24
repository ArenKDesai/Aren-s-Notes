#CS537 #UWMadison #OperatingSystems 

Developer-made processes need to utilize a computer's memory in order to function. However, the physical locations of memory are hidden by the OS, so memory is virtualized ([[Virtualization]]). So how does the OS efficiently handle allowing processes to allocate virtual memory?

## Dynamic Relocation
The first idea is to take the process
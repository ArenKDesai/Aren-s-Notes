#CS537 #UWMadison #OperatingSystems 

Developer-made processes need to utilize a computer's memory in order to function. However, the physical locations of memory are hidden by the OS, so memory is virtualized ([[Virtualization]]). So how does the OS efficiently handle allowing processes to allocate virtual memory?

## Base and Bounds
The first idea is to take the process's memory and place it into physical memory like placing a peg into a hole. This idea allows the hardware to fully handle address translation, a notion known as **base and bounds**, or dynamic relocation. 
CPU needs two hardware registers: the **base register** and the **bounds register** (or limit register). 
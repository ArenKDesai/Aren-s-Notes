A process is a running program. We typically want multiple processes running at once (web browser, music streamer, game, etc.), so we virtualize the CPU and allow time sharing of the virtualized CPU so the processes can be started, stopped, and started again. 
Virtualization of the CPU is supported by mechanisms, low-level methods or protocols that implement a needed piece of functionality. 
The memory that a process can access is its address space, supported by registers that can be read and uploaded to very frequently. 
The program counter (PC), or instruction pointer (IP), keeps track of which instruction of the program will execute next. The stack pointer and frame pointer manage the stack for function parameters, local variables, and return addresses. 

## Process API
These APIs are generally available on any OS:
1. Create: create new processes. 
2. Destroy: forcefully shut down a process. 
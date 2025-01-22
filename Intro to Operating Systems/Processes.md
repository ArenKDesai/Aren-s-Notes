A process is a running program. We typically want multiple processes running at once (web browser, music streamer, game, etc.), so we virtualize the CPU and allow time sharing of the virtualized CPU so the processes can be started, stopped, and started again. 
Virtualization of the CPU is supported by mechanisms, low-level methods or protocols that implement a needed piece of functionality. 
The memory that a process can access is its address space, supported by registers that can be read and uploaded to very frequently. 
The program counter (PC), or instruction pointer (IP), keeps track of which instruction of the program will execute next. The stack pointer and frame pointer manage the stack for function parameters, local variables, and return addresses. 

## Process API
These APIs are generally available on any OS:
1. Create: create new processes. 
2. Destroy: forcefully shut down a process. 
3. Wait: pause execution until a certain process is done running. 
4. Misc. Control: other options, like suspending a process and resuming it. 
5. Status: Information on a process for long it has run, what state it is in, etc. 

### Process Creation
To create a program, an OS must first load its code and any static data into memory / the address space of the process. Processes are typically stored as bytes on a hard drive (HD) or solid-state drive (SSD). Modern OSes perform the process lazily bu loading pieces of code or data only as they are needed during program execution. 
Some memory must also be allocated for the program's stack and heap. 

### Process States
Processes can be in one of three simplified states:
1. Running: executing instructions
2. Ready: prepared to run but not yet executed
3. Blocked: executed some operation and waiting for an external event before it can continue running
Moving from ready to running means a process has been scheduled, while running to ready means descheduled. 
Direct execution is when a process (see [[Processes]]) runs on the CPU. This entails creating a process entry in the process list, allocating memory for it, loading the program code from disk into memory, locating the entry point (usually ```main()```), jumping to that point in the address space, and running the user's code. This is very fast, but introduces problems with operating system (OS) support, such as when a process needs to issue I/O operations. 
To avoid this, we introduce user mode. This is restricted code that can't issue I/O requests. In contrast, there is kernel mode, which is the mode the OS or kernel runs in. There are no restrictions for kernel mode. Instead, user programs must use system calls. 

## System Calls and Traps
In user mode, I/O operations and other blocked actions are done through system calls, which initiate trap instructions. This temporarily raises the privilege level to kernel mode. An instruction called return-from-trap is called after. 

At boot time, the kernel sets up a trap table in kernel mode that specifies what code to run during certain exceptional events (trap handlers). 
A system-call number is typically assigned to each system call. The user code is responsible for placing the desired system-call number in a register or at a specified location on the stack. Since the code cannot jump to an address itself, the kernel code is safe from malware. 

## Protocol
LDE protocol has two phases:
1. The kernel initializes trap table and the CPU uses a privileged instruction to remember the address. 
2. The kernel sets up other necessary processes (allocating a node o)
#UWMadison #OperatingSystems #CS537 

Moore's law is dead, and now we just pile more cores into the same processor. This means we need a way to allow applications to use multiple cores at the same time. 
One option is building an app with separated logical processes, and using pipes to transfer the data between the process. However, this includes a lot of overhead with copying memory. Context switches are also more expensive since each process has it's own page table, which is more page faults. 

We'll introduce the concept of a thread. These have stacks and stack pointers, program counters, etc. However, multiple threads share the same address space, code, heap, PIDs, etc. Depending on the OS, these may run on one core or multiple cores. 
There are multiple ways to program with threads:
1. Producer / Consumer. Some nodes are producing, some are consuming. Think ROS2 or [[Kafka]]. 
2. Pipeline: The task is a series of subtasks, each of which is handled by its own thread. 
3. Defer work with background thread. Non-critical work is done in the background while the CPU is idle. 

To create threads, processes have options depending on their OS. One of those is POSIX Pthreads. 
Common thread operations include create, exit, and join, but there is no fork. 

### Thread Operations
One model of thread control is keeping thread capabilities to the user, who can add and control threads via a library. The OS is not aware of these user-level threads, and these threads can be very fast. However, since one user typically doesn't spin up multiple processes, there cannot be multiple threads on different cores. Also, when one thread blocks, the entire process blocks. 

Another model is kernel-level threads. Each user-level thread is a kernel thread, and each kernel thread is scheduled independently. thread operations are fully performed by the operating system. This is nice since the kernel-level threads can run in parallel on a multiprocessor and one thread blocking doesn't block the other threads. However, thread operations do have high overhead, and the OS must scale to support that number of threads. 
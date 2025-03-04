#UWMadison #OperatingSystems #CS537 

Moore's law is dead, and now we just pile more cores into the same processor. This means we need a way to allow applications to use multiple cores at the same time. 
One option is building an app with separated logical processes, and using pipes to transfer the data between the process. However, this includes a lot of overhead with copying memory. Context switches are also more expensive since each process has it's own page table, which is more page faults. 

We'll introduce the concept of a thread. These have stacks and stack pointers, program counters, etc. However, multiple threads share the same address space, code, heap, PIDs, etc. Depending on the OS, these may run on one core or multiple cores. BTW, every core has its own PTBR. 
There are multiple ways to program with threads:
1. Producer / Consumer. Some nodes are producing, some are consuming. Think ROS2 or [[Kafka]]. 
2. Pipeline: The task is a series of subtasks, each of which is handled by its own thread. 
3. Defer work with background thread. Non-critical work is done in the background while the CPU is idle. 

To create threads, processes have options depending on their OS. One of those is POSIX Pthreads. 
Common thread operations include create, exit, and join, but there is no fork. 

### Thread Operations
One model of thread control is keeping thread capabilities to the user, who can add and control threads via a library. The OS is not aware of these user-level threads, and these threads can be very fast. However, since one user typically doesn't spin up multiple processes, there cannot be multiple threads on different cores. Also, when one thread blocks, the entire process blocks. 

Another model is kernel-level threads. Each user-level thread is a kernel thread, and each kernel thread is scheduled independently. thread operations are fully performed by the operating system. This is nice since the kernel-level threads can run in parallel on a multiprocessor and one thread blocking doesn't block the other threads. However, thread operations do have high overhead, and the OS must scale to support that number of threads. 

## Locks
So, there's a problem we need to address. We want to avoid "Heisenbugs" (bugs from non-deterministic concurrency), so we turn to atomic code in uninterruptable groups. This can be done by sectioning code into **critical sections** that cannot have multiple threads changing variables. 

We want to provide **mutual exclusion**, so only one thread can be in a region at a time (like a single-user bathroom). This is where a lock comes in. A developer can create a lock with:
```C
Pthread_mutex_t mylock = PTHREAD_MUTEX_INITIALIZER;
```
The lock can be **acquired** or **locked** by a thread, in which case other threads will need to wait for the lock to be **unlocked** or **released**. This can be done with:
```C
Pthread_mutex_lock(&mylock);
Pthread_mutex_unlock(&mylock);
```
While waiting, the thread either blocks or spins the CPU. 

While locking, we target three goals:
1. Mutual exclusion. Only one thread can be in a critical section at a time. 
2. **Progress** (deadlock-free). We want to make sure that at least one thread is making progress. We don't want threads stuck on a locked section forever. 
3. **Bounded** (starvation-free). Similar to above, allow all threads to enter. 

There are a few methods to implement locking. One is to disable interrupts during critical sections. This is very fast, but only works on uniprocessors. The OS also cannot perform other necessary work. 
Another method is using load and store commands. The acquire function has a variable labeled False, sets it to true in a permanent loop, and waits until another process sets this to false. This doesn't really work since having >2 threads can cause serious issues. This is not atomic. 
Since none of these methods really work, we'll have the hardware work the load/store operation (since the hardware cannot be interrupted). This is done with ```xchg```, which replaces a variable's value with a value, but returns the old value. Set it to 1 in a loop, and if it returns 0 instead of 1, the lock was released. 

Schedulers are unaware of locks and unlocks, so processes can take advantage of basic spinlocks to permanently lock other processes. However, we can give locks a **ticket**, like a bakery. This is a new command called ```FetchAndAdd```. This is a **hardware primitive** that finds an old value, adds one to it, and returns the new value. 
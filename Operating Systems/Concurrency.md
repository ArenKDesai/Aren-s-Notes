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

**Condition variables**: queue of a waiting threads. A process waits by adding itself to the queue with the ```wait``` function. Another function calls ```signal``` for the first process to run. 

This can cause problems if a process sets the ```done```variable to 1 before a process actually calls ```wait```. 

One attempt at fixing this is keeping state variables that can be checked continuously. This is locking with ```Mutex_lock``` and waiting, while the child sends both the signal to unlock *and* the signal to wake up. 
This breaks when the child doesn't acquire the lock. Notifying a thread that it's done without taking a lock is called a **naked lock**. 

## Pipes
Pipes can have multiple writers and readers (like [[Kafka]]). The pipe has an internal finite-sized buffer, and the writers are blocked if the pipe is full / readers are blocked if the pipe is empty. 

The buffer has a start and end pointer. When a write occurs, the end pointer moves. When a read occurs, the start pointer moves. When the end pointer is at the end, it wraps around unless the buffer is full. This looks similar to a loading bar. 

### Producer
While running, the producer locks and waits if the buffer is full. If not full, it fills the buffer, signals (in case the reader is waiting), and unlocks. 

### Reader (AKA Consumer)
While running, the reader locks, waits if the buffer is empty. If not, it grabs the new data, signals (in case producer is waiting), unlocks, *then* pushes data. 
This can cause problems if 1. there are multiple readers, and 2. a reader acquired the lock first. This would cause the reader to receive the signal instead of the producer, and the producer would never be woken up. This is fixed by always using a ```while``` loop rather than an ```if``` statement. 
A more concrete way to fix this problem is keep the conditional statements checking two condition variables instead of one: full and empty. 

## Deadlock
Occurs when multiple threads are waiting on each other. Similar to a four-way intersection where cars from all four sides are blocking each other. Also similar to circular dependencies. 
For example, imagine one thread locks A, then B. Another thread locks B, then A. This can cause **deadlocking**, where the fix would be to reorder the locks. 
This is often a problem in **encapsulating**, where you abstract data structures, and reversed orderings is possible. A fix for this is to manually ensure there is some order, such as ordering from high->low addresses. 

There are four conditions for deadlocks:
1. Mutual exclusion (don't even use locks; use comparisons instead)
2. Hold-and-wait (acquire all atomic locks under one **meta lock**)
3. No preemption (can't take lock away; causes **livelock** where no processes can make progress, like deadlock but the processes are not waiting)
4. Circular wait
which also means that, if we eliminate one of these, we don't have to worry about deadlock anymore. 

## Semaphores
Semaphores are primitives designed to handle concurrency. They can be thought of as integers with three special routines:
1. `sem_init`: Initialize the semaphore. 
2. `sem_wait`:  Similar to acquiring a lock. Decreases the value of the semaphore by one, and waits if the value of the semaphore is negative. 
3. `sem_post`: Similar to releasing a lock. Increases the value of the semaphore by one and wakes a thread if one is waiting. 
Semaphores need to be initialized with an in-place `sem_t` (the integer-holding variable), the number 0, and the integer to initialize the semaphore to. 

It's generally good to imagine the number the semaphore is initialized to as the number of resources you're immediately willing to give away.

When the value of the semaphore is negative, it's equal to the number of waiting threads. 
Example:
```C
sem_t m;
sem_init(&m, 0, X); // X is integer, like 

sem_wait(&m);
// critial section
sem_post(&m);
```

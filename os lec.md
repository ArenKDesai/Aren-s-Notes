We want to avoid "Heisenbugs" (bugs from non-deterministic concurrency), so we turn to atomic code in uninterruptable groups. This can be done by sectioning code into **critical sections** that cannot have multiple threads changing variables. 

## Locks
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
Another method is using load and store commands. The acquire function has a variable labeled False, sets it to true in a permanent loop, and waits until another process sets this to false. This doesn't really work since having 
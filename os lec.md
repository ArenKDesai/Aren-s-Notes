We want to avoid "Heisenbugs" (bugs from non-deterministic concurrency), so we turn to atomic code in uninterruptable groups. This can be done by sectioning code into critical sections. 

## Locks
We want to provide **mutual exclusion**, so only one thread can be in a region at a time (like a single-user bathroom). This is where a lock comes in. A developer can create a lock with:
```C
Pthread_mutex_t mylock = PTHREAD_MUTEX_INITIALIZER;
```
The lock can be **acquired** or **locked** by a thread, in which case other threads will need to wait for the lock to be **unlocked** or **released**. 
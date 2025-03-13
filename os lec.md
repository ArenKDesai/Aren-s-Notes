## Semaphores
Semaphores are primitives designed to handle concurrency. They can be thought of as integers with three special routines:
1. `sem_init`: Initialize the semaphore. 
2. `sem_wait`:  Similar to acquiring a lock. Decreases the value of the semaphore by one, and waits if the value of the semaphore is negative. 
3. `sem_post`: Similar to releasing a lock. Increases the value of the semaphore by one and wakes a thread if one is waiting. 
Semaphores need to be initialized with an in-place `sem_t` (the integer-holding variable), the number 0, and the integer to initialize the semaphore to. 

It's generally good to imagine the number the semaphore is initialized to as the number of resources you're immediatelly willing to give away.

When the value of the semaphore is negative, it's equal to the number of waiting threads. 
Example:
```C
sem_t m;
sem_init(&m, 0, X); // X is integer, like 1

sem_wait(&m);
// critial section
sem_post(&m);
```

### Producer/Consumer (Bounded Buffer) Problem
Having a producer / consumer situation can be tricky with semaphores. 
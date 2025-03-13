## Semaphores
Semaphores are primitives designed to handle concurrency. They can be thought of as integers with three special routines:
1. `sem_init`: Initialize the semaphore. 
2. `sem_wait`:  Similar to acquiring a lock. Decreases the value of the semaphore by one, and waits if the value of the semaphore is negative. 
3. `sem_post`: Release lock. 
Semaphores need to be initialized with an in-place `sem_t` (the integer-holding variable), the number 0, and the integer to initialize the semaphore to. 
## Semaphores
Semaphores are primitives designed to handle concurrency. They can be thought of as integers with three special routines:
1. `sem_init`: Initialize the semaphore. 
2. `sem_wait`:  Acquire a lock. 
3. `sem_post`: Release lock. 
Semaphores need to be initialized with an in-place `sem_t`
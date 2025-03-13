## Semaphores
Semaphores are primitives designed to handle concurrency. They can be thought of as integers with two special routines:
1. `sem_wait`:  Acquire a lock. 
2. `sem_post`
## Review
Condition variables: queue of a waiting threads. A process waits by adding itself to the queue with the ```wait``` function. Another function calls ```signal``` for the first process to run. 

This can cause problems if a process sets the ```done```variable to 1 before a process actually calls ```wait```. 

One attempt at fixing this is keeping state variables that can be checked continuously. This is locking with ```Mutex_lock``` and waiting, while the child sends both the 
This breaks when the child doesn't acquire the lock. Notifying a thread that it's done without taking a lock is called a **naked lock**. 


## Review
Condition variables: queue of a waiting threads. A process waits by adding itself to the queue with the ```wait``` function. Another function calls ```signal``` for the first process to run. 

This can cause problems if a process sets the ```done```variable to 1 before a process actually calls ```wait```. 

One attempt at fixing this is keeping state variables that can be checked continuously. This is locking with ```Mutex_lock``` and waiting, while the child sends both the signal to unlock *and* the signal to wake up. 
This breaks when the child doesn't acquire the lock. Notifying a thread that it's done without taking a lock is called a **naked lock**. 

### Pipes
Pipes can have multiple writers and readers. The pipe has an internal finite-sized buffer, and the writers are blocked if the pipe is full / readers are blocked if the pipe is empty. 

The buffer has a start and end pointer. When a write occurs, the end pointer moves. When a read occurs, the start pointer moves. When the end pointer is at the end, it wraps around unless the buffer is full. This looks similar to a loading bar. 
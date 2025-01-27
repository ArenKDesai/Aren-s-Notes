We need to figure out how to schedule jobs for the CPU. This is extremely similar to some of the algorithms covered in [[Greedy]] and [[Dynamic Programming]]. 

We need to target a scheduling metric. One of those is turnaround time, or the time at which the job completes minus the time at which the job arrived in the system. Another is fairness from Jain's Fairness Index. 
An example of average turnaround time is three jobs arriving at 0, each taking 10 seconds

First is FIrst In, First Out (FIFO). This was also covered in [[Caches]]. 
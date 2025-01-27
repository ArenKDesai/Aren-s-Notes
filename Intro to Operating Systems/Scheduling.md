We need to figure out how to schedule jobs for the CPU. This is extremely similar to some of the algorithms covered in [[Greedy]] and [[Dynamic Programming]]. 

## Algorithms
We need to target a scheduling metric. One of those is turnaround time, or the time at which the job completes minus the time at which the job arrived in the system. Another is fairness from Jain's Fairness Index. 
An example of average turnaround time is three jobs arriving at 0, each taking 10 seconds. The average turnaround time is $\frac{10+20+30}{3}=20$. 
FIrst In, First Out (FIFO) organizes jobs sequentially. This was also covered in [[Caches]]. This can be problematic with the **convoy effect**, which occurs when one job at the beginning inflates the average turnaround time. 
Another algorithm is Shortest Job First (SJF). SJF is optimal. However, if jobs can arrive at any time (not just time 0), then it fails. 
Then, we need Shortest Time-to-Completion First (STCF), which is a **preemptive** scheduler that can context-switch to another process. 


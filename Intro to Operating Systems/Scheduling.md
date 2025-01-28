We need to figure out how to schedule jobs for the CPU. This is extremely similar to some of the algorithms covered in [[Greedy]] and [[Dynamic Programming]]. 

## Algorithms
We need to target a scheduling metric. One of those is turnaround time, or the time at which the job completes minus the time at which the job arrived in the system. Another is fairness from Jain's Fairness Index. 
An example of average turnaround time is three jobs arriving at 0, each taking 10 seconds. The average turnaround time is $\frac{10+20+30}{3}=20$. 

### Basics
FIrst In, First Out (FIFO) organizes jobs sequentially. This was also covered in [[Caches]]. This can be problematic with the **convoy effect**, which occurs when one job at the beginning inflates the average turnaround time. 
Another algorithm is Shortest Job First (SJF). SJF is optimal. However, if jobs can arrive at any time (not just time 0), then it fails. 
Then, we need Shortest Time-to-Completion First (STCF), which is a **preemptive** scheduler that can context-switch to another process. 
Once interactive terminals were created, response time became the next problem. At this point, we employ Round-Robin (RR) scheduling. RR is a **fair** algorithm that schedules all processes evenly. 
Preemptive algorithms benefit from **overlap**, where a context switch can occur while a process is waiting I/O communication. 

### Multi-level Feedback Queue
One of the best-known solutions for scheduling is **Multi-level Feedback Queue (MLFQ)**. The MLFQ has multiple distinct queues with different priority levels. MLFQ uses these priority levels to decide which job should run. There are two rules:
1. If Priority(A) > Priority(B), A runs and B doesn't
2. Priority(A) = Priority(B), A and B run RR
MLFQ then varies a process's priority based on its observed behavior. This is done with **allotment**, the amount of time a job can spend at a given priority before its priority is reduced. There are thus three more rules:
1. When a job enters the system, it is placed at the highest priority. 
2. If a job uses up its allotment while running, its priority is reduced. 
3. If a job gives up the CPU (like I/O operations) before allotment is up, it stays at the same priority level. 

The first major problem is **starvation**, where too many interactive 
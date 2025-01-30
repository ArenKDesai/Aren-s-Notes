We need to figure out how to schedule jobs for the CPU. This is extremely similar to some of 
the algorithms covered in [[Greedy]] and [[Dynamic Programming]]. 
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
3. When a job enters the system, it is placed at the highest priority. 
4. If a job uses up its allotment while running, its priority is reduced. 
5. If a job gives up the CPU (like I/O operations) before allotment is up, it stays at the same priority level. 

The first major problem is **starvation**, where too many interactive jobs will consume all CPU time. The second is that a user could game the system by issuing an I/O command just before allotment is up. This introduces rule 6:
6. After some time period, move all jobs to the topmost queue

### Proportional / Fair Share
The proportional or fair share scheduler is known as a lottery scheduler. Tickets are used to represent the share of a resource that a process should receive. The randomness is a feature since it means the scheduler cannot be abused. 
One mechanic is **ticket currency**, where users can allocate their processes a certain amount of currency. Another is **ticket transfer**, where a process can temporarily hand off tickets to another process. Sometimes, a process is also allowed to cause **ticket inflation** and raise or lower the number of tickets it owns. 
To avoid randomness, **stride scheduling** was invented. This technique considers each job to have a stride, which is inverse in proportion to the number of tickets it has. 

### Linux Completely Fair Scheduler
The current Linux approach is the CFS, which aims to decrease scheduler decision-making overhead as much as possible. It does this by tracking the **virtual runtime (vruntime)** of every process. As a process runs, it accumulates vruntime, and CFS will pick a process with the lowest vruntime to run next. 
CFS manages the decision on when to context switch through a control parameter **sched_latency**, which tracks the amount of time a process can run maximum before a switch. This value can be lowered when there is more processes, but no less than another control parameter **min_granularity**. 
CFS keeps all processes in a red-black tree. 

## Multiprocessor Scheduler
Accessing memory from another processor can be expensive, so there's often a global queue for all jobs. All CPUs pull from the global queue. This has low response time and allows for global priorities to move high-priority jobs to CPUs running low-priority jobs, but communication is expensive, and cache locality is lost when a job moves between CPUs. 
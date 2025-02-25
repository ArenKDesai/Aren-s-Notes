An operating system (OS) abstracts and manages hardware resources for applications. Provides a set of utilities to simplify app development. 
These resources include CPU, volatile storage (disks), network comms, I/O devices, etc. 
Operating systems take care of virtualization, concurrency, and persistence. They promote the usage of hardware resources through OS policies. These polices are aimed at rescheduling processes for fairness and efficiency. Earliest deadline first (the [[Greedy]] algorithm) is an example of this. 

The OS provides a standard library of a few hundred system calls that are available to applications. 

Multiple programs can be run at the same time with threads, which can be considered functions with that share a memory space with other functions. 

The OS **doesn't** virtualize the disk. It virtualizes the other hardware for ease-of-use and memory management. 

Programs are passive: it's code + data. A process is running a program. 
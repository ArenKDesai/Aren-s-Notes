## RAID
We have one disk, but as with many things in computer science, more might be better. Can we use multiple disks to improve the **capacity**, **performance**, and **reliability** of the system?
For the Operating System, the disk is abstracting to a linear array. This means that multiple disks can be set up to extend the linear array without any extra work on the OS's side. This is a redundant array of independent disks (RAID) system. 
A RAID system includes its own RAID controller, a physically separate device, typically connected via SATA or PCIe. 

So, we have an array of disks. How do we map blocks in the linear array to disks in the RAID?
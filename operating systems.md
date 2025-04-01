## RAID
We have one disk, but as with many things in computer science, more might be better. Can we use multiple disks to improve the **capacity**, **performance**, and **reliability** of the system?
For the Operating System, the disk is abstracting to a linear array. This means that multiple disks can be set up to extend the linear array without any extra work on the OS's side. This is a redundant array of independent disks (RAID) system. 
A RAID system includes its own RAID controller, a physically separate device, typically connected via SATA or PCIe. 

So, we have an array of disks. How do we map blocks in the linear array to disks in the RAID? There are a few options:
1. RAID 0: "striping". We distribute the blocks evenly. Disk 1 gets the first block, disk 2 gets the second, disk 3 gets the third, etc. This loops around when we run out of disks. If there's three disks, 
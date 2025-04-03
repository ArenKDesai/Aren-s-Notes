#UWM
## I/O Devices
The CPU and RAM are connected to the memory bus, which rests on the general I/O bus. The graphics is connected to the general pus. Data, such as from a USB, is on the peripheral bus. 
**PCIe** is the (common) bus that can interact with the CPU through the **I/O chip**. It's typically the connection between the CPU and the network. 
**eSATA** is the same thing but with disks instead of network. 
Devices like the keyboard and mouse can interact directly with I/O chip. 

### The Canonical Device Diagram
A device has registers: **status**, **command**, and **data**. The OS can use load/store instructions on the physical address space of the devices through these registers. These registers are available to the OS. 
The device also has hidden internals, including a CPU and RAM. Depending on the device, this is often a microcontroller. 

A write protocol looks similar to an exchange lock ([[Concurrency]]). Wait for status to not be busy, write data, write command, and wait again. These wait instructions often wait for an interrupt so someone else can use the CPU. 
This introduces a tradeoff. Are interrupts better than polling? 
If the device is fast, the overhead from an interrupt can be more time than the polling. If the device is slow or the time is unknown, than either interrupts or a hybrid approach works. Sometimes, if network cards are too fast and there are too many interrupts, the CPU can spend all its time on interrupt handling. In this case, we can ignore the interrupt handler for a bit. Another option is **interrupt coalescing**, or bundling interrupts together and writing to the data / command registers for multiple interrupts at a time. 

Example:
```
while (STATUS == BUSY)
	wait for interrupt;
write data to DATA register;
write command to COMMAND register;
while (STATUS == BUSY)
	wait for interrupt;
```

### Data Protocol
There are two paradigms: Programmed I/O or Direct Memory Access. 
Programmed I/O (PIO) is where the CPU directly tells the device what the data is. 
Direct Memory Access (DMA) is where the CPU leaves the data in memory, and the device reads that data from memory. This transfer the reading cost from the CPU to the device. DMA removes the "write data to the DATA register" step on the device's main loop. 

Another option is having an I/O queue. In the queue, you enter the description of your command (read, write, etc). The OS can aggregate the commands in the queue. 

### Device Drivers
Each device has it's own I/O specifications. These are described in device drivers. The OS uses these device drivers to talk with the device. 

### Hard Drives
Hard drives (HDs) include the disk (which holds the data) and the arm (which writes the data). The time it takes for the arm to write the data includes the seek, rotation, and transfer time. In other words, the arm must position itself and slow down, the disk must rotate, and the arm must write. 
Seek time is ~4 milliseconds. Rotation is 4-8 milliseconds. Transfer is ~5 milliseconds per gigabyte (which is mostly arbitrary). 
When the disk head (or arm head) is in the wrong place, it is 3,400x slower to reach the correct location. 

### Solid State Drives
Solid state drives (SSDs) include a NAND flash block, which is a grid of cells. There are three levels:
1. Single Level Cell (SLC): 1 bit per cell (fast, reliable)
2. Multi Level Cell (MLC): 2 bits (slower, less reliable)
3. Triple Level Cell (TLC): 4 bite (even more so)
Writing to the SSD consists of erasing (setting all bits to 1) and programming (clearing some bits). Re-writing a block, even in partial, requires the device to clear the entire block. This works in one page at a time. 
Reading an SSD is a NAND operation with a page selection. This is 100x faster than a write operation. 

## RAID
We have one disk, but as with many things in computer science, more might be better. Can we use multiple disks to improve the **capacity**, **performance**, and **reliability** of the system?
For the Operating System, the disk is abstracting to a linear array. This means that multiple disks can be set up to extend the linear array without any extra work on the OS's side. This is a redundant array of independent disks (RAID) system. 
A RAID system includes its own RAID controller, a physically separate device, typically connected via SATA or PCIe. 

So, we have an array of disks. How do we map blocks in the linear array to disks in the RAID? We'll denote the number of disks as $N$ and the capacity in gigabytes as $D$. The random performance of the disk is $R$ and the sequential is $S$. There are a few options:
1. **RAID 0**: "striping". We distribute the blocks evenly. Disk 1 gets the first block, disk 2 gets the second, disk 3 gets the third, etc. This loops around when we run out of disks. If there's three disks, the fourth block goes to disk 1. This capacity is $N\times D$, and read/write performance are both $R$ time. The **throughput**, or stream of requests, for random requests is $N\times R$, while the sequential throughput is $N\times S$. Finally, this system is *not* reliable. If one disk fails, we lose all disks. In fact, since we have multiple disks rather than one, RAID 0 has less reliability than a single disk. The **mean time to failure (MTTF)** is 3 years. These are independent and can be summed; if there are 10 disks, after one year, there's a $\frac{10}{3}$ chance of failure. 
2. **RAID 1** (sometimes called RAID10). We use RAID 0, but we duplicate data. With four disks, the first block goes to both disks 1 and 2, the second block goes to 3 and 4, the third goes to 1 and 2, etc. The capacity is $D\times \frac{N}{2}$. Reliability is much better. We can tolerate at least one failure. The MTTF is 3000 years. The latency performance is $R$ for read and writes, and the throughput is for random reads is $N\times R$. This is twice as good as RAID 0 because the data is duplicated once. The throughput for random writes is $\frac{N\times R}{2}$. Sequential writes are $\frac{N\times S}{2}$ and sequential reads are $\frac{N\times S}{2}$. 
3. **RAID 4**: "parity". We store enough info on one disk to recover from failure. If you have five disks, you can use four for data (using striping) and the last disk as the parity disk. If you imagine whether a block is allocated on a disk as a boolean, you perform an XOR on the stripe. Capacity is $(N-1)\times D$, reliability can tolerate one failure. Random reads are $(N-1)\times R$, sequential reads are $(N-1)\times S$, sequential writes are $(N-1)\times S$. Random write performance is calculated with **additive parity**: read an entire stripe, compute the new parity, and write the new block and parity block. Or, it can be calculated with **subtractive parity**: read the old block and old parity, compare the old and new block, and compute the new parity based on that comparison. In other words, $P_\text{new}=(B_\text{old}+B_\text{new})+P_\text{old}$. This requires 2 reads and 2 writes, and the parity disk must *always* be written to, so it becomes a bottleneck. Our random write throughput is $\frac{R}{2}$ regardless of the disk count. 
4. **RAID 5**: "distributed parity". We distribute parity across all disks instead of one parity disk. This somewhat looks like the diagonal of a square matrix, but going from top-right to bottom-left, where each of the diagonal entries are the parity information. Capacity is $(N-1)\times D$, reliability can tolerate one failure. Sequential reads are $(N-1)\times S$, sequential writes are $(N-1)\times S$, random reads are $N\times R$, and random writes are $\frac{N}{4}\times R$. 
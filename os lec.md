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
Writing to the SSD consists of erasing (setting all bits to 1) and 
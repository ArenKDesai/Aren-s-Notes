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
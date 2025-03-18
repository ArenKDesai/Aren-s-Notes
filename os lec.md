## I/O Devices
The CPU and RAM are connected to the memory bus, which rests on the general I/O bus. The graphics is connected to the general pus. Data, such as from a USB, is on the peripheral bus. 
**PCIe** is the (common) bus that can interact with the CPU through the **I/O chip**. It's typically the connection between the CPU and the network. 
**eSATA** is the same thing but with disks instead of network. 
Devices like the keyboard and mouse can interact directly with I/O chip. 

### The Canonical Device Diagram
A device has registers: **status**, **command**, and **data**. The OS can use load/store instructions on the physical address space of the devices through these registers. These registers are available to the OS. 
The device also has hidden internals, including a CPU and RAM. Depending on the device, this is often a microcontroller. 

A write protocol looks similar to an exchange lock ([[Concurrency]]). Wait for status to not be busy, write data, write command, and wait again. These wait instructions often wait for an interrupt so someone else can use the CPU. 
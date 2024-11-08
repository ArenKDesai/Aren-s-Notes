#CS354 #C #Exceptions #UWMadison

### The four exceptions
Traps
- Synchronous
- Always return to the next instruction
- Allow the user to request the kernel to do some work
- Example: A Linux command shell creates a new process
Interrupts
- Asynchronous
- Always return to the next instruction
- SIGINT
- Example: A network adaptor card receives a data packet
- Always I/O
Aborts
- Synchronous
- Does not return
- Example: The system's main memory malfunctions
Fault
- Synchronous
- Might return to current instruction
- Example: dereferencing a null pointer


We want to create an abstracted memory space that starts at address 0 and goes until a specific finite address. 

If a process is in a lower physical space than another program, it can overwrite memory in the other program. 

Having a base and bounds for protecting memory is useful to keep programs secure, but easily leads to fragmentation. 

This leads us into segmented addressing, where the process specifies the segment and offset within the segment. The first two bits in a segment table is the offset, and
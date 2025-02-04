We want to create an abstracted memory space that starts at address 0 and goes until a specific finite address. 

If a process is in a lower physical space than another program, it can overwrite memory in the other program. 

Having a base and bounds for protecting memory is useful to keep programs secure, but easily leads to fragmentation. 

This leads us into segmented addressing, where the process specifies the segment and offset within the segment. The first two bits in a segment table is the offset, and the last 12 is the address. 

For example, if the address is 0x0240 and the segment table has base 0x2000 on segment 0, you end with 0x2240. 

Offsets for memory structures that grow down, like the stack, need a special equation (negative offset) to find the physical addresses. 

With segmentation, we avoid internal segmentation b
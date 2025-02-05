The easiest form of storing memory is base-and-bounds, where each memory block is allocated the same amount in a set. However, if a process needs more space then we have, the operating system would crash. This means we need to **segment** memory. 
These segments store information on the amount of allocated bytes, which helps the hardware know when to throw a segmentation fault. 

We also want to support sharing, so protection bits label the "read, write, execute"-ability of a segment. 

Systems with just a few segments are coarse-grained. However, fine-grained systems have existed for a long time as well. 

When there's too many segmentations leaving small bits of memory that aren't big enough to use, that's **external fragmentation**. The best fix to this would be to re-arrange the memory. 
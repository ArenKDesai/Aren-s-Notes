### SSDs
- Slow for 1GHz devices
- use chips fabricated similarly to CPUs
- speeds closer to CPUs
- No mechanical parts, use transistors
- NAND-based technology
- Higher cost per bit than hard drives, but better performance
- contains blocks made of pages
- Writing a single page requires erasing the entire block of pages
- a block is likely to fail after a certain number of erases (1000 for slow/high density, 100,000 for fast/low density)

#### Striping
- block addresses striped across flash packages
- a single request can span multiple chips
- has natural load balancing

#### Operations
- Reading a page involves retrieving the contents of an entire page which can be 25-75 microseconds
- erasing a block resets each page in the block to all 1s. cost is 1.5-4.5 miliseconds. This is much more expensive than reading. 
- writing a page is changing bits from 1 to 0, and the cost is 200-1400 microseconds. Slower than read, faster than erase. 

### NAND
A NAND flash block is a grid of cells, of the following:
- Single Level Cell: 1 bit per cell (fast, more reliable)
- Multi Level Cell: 2 bits per cell (slower, less reliable)
- Triple Level Cell: 4 bits per cell (even more so)
- Erase: set all bits to 1
- Program: clear some bits
- read: NAND operation with a page selected

### Flash Translation Layer
We want to translate reads/writes to logical blocks into reads/erases/programs on physical pages+blocks
We also want to reduce write amplification, or the amount of extra copying needed to deal with block-level erases
We also want to implement wear leveling, or distributing writes equally to all blocks to avoid fast failures of a "hot" blocks

## RAID
### 0
Capacity: $N*C$
Safely lose disks: 0
Random Latency: $D$
Throughput: $N*S, N*R$
### 1
Capacity: $N/2*C$
Safely lose disks: min: 1, max: $N/2$
Latency: $D$
Throughput
random reads: $N*R$
random writes: $N/2*R$
sequential writes: $N/2*S$
sequential reads: $N/2*S$

### 4
Parity disk

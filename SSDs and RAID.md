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
- Reading a page involves retrieving the contents of an entire page which can be 25-75 miliseconds

### NAND
A NAND flash block is a grid of cells, of the following:
- Single Level Cell: 1 bit per cell (fast, more reliable)
- Multi Level Cell: 2 bits per cell (slower, less reliable)
- Triple Level Cell: 4 bits per cell (even more so)
- Erase: set all bits to 1
- Program: clear some bits
- read: NAND operation with a page selected

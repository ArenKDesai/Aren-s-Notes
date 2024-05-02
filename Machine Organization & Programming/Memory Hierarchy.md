#C #CS354 #Memory #Cache #UWMadison

### Replacement policies
Least frequently used - save *k* ways (spots), mark them when they're used, replace the least used spot

###  Locality
Temporal locality - Efficient re-grabbing of data, like caches
- Example: Repetition Control Flow
- Non-Example: Linear Search on an array of integers
- Non-Example: Accessing the first element of each row in a 2D array that is heap allocated as an array of arrays
Spatial locality - Efficient memory placement, like iterating rows - columns instead of vice versa

### CODE

### DATA
.bss --> uninitialized variables
.data --> initialized global variables

### STACK

## HEAP
Internal fragmention --> block padding, block headers. Occurs when you need to pad a heap block. 
External fragmentation --> Occurs when there is enough free space to fit a heap block, but due to free space allocation, it cannot fit. 

### Multidimensional arrays
[[Basic C]]
int a\[2]\[3]\[4]
1. Start with the lowest dimension
2. \[4] = \[]\[]\[]\[]
3. move to second lowest
4. \[3] = \[4]\[4]\[4]
5. Then move to full model with dimension 1-n
6. a\[1]\[0]\[3] = 0x100C + 0x3C = 0x1048
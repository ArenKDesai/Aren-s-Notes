#Algorithms #CS577 #UWMadison #CountSort

Use recursion to split a problem into smaller sub-problems. Typically used to improve the efficiency of already efficient algorithms, like sorting going from $O(n^2)$ to $O(n\log n)$. 
These usually abide by program correctness: show that the program is sound and complete. 
## Examples

### Discussion Example

You are given $2^s$ many arrays of sorted int, each with size $n$. We want to combine them into large sorted array in $O(s2^sn)$

What is the algo?
Algorithm: 2nd half of mergeSort. Take the lowest level of the mergeSort tree and merge upwards. This is $s2^sn$, as there are $s$ levels and at most $2^s$ nodes with length $n$. 

What is the recurrance relation for runtime in terms $n,s$?
Start w/ $2^s$ n-arrays, move to $2^{s-1}$ many 2n-arrays. 
$T(n,s) = T(2n,s-1)+2^sn$
$T(n,0)=1$

### Discussion Example 2

Given $n\cdot n$ grid, there is a number in each box (assume all numbers are distinct). Call a box local minimum if it is smaller than all its neighbors (up, down, left, right). Find a local min in $O(n)$ time. 

### CountSort

Recursion:
$C(n)=2C(\frac{n}{2})+2n$
Note: mergeCount is $O(2n)$. 

The cost sum is $\sum_{i=0}^k2^i2n/2^i$. $2n$ can be factored out, and the geometric series can be recalculated for $2nk+k$, where $k$ is $2\log n+1$, so the algorithm is $O(n\log n)$. 
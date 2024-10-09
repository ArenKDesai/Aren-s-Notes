#Algorithms #CS577 #UWMadison #CountSort

Use recursion to split a problem into smaller sub-problems. Typically used to improve the efficiency of already efficient algorithms, like sorting going from $O(n^2)$ to $O(n\log n)$. 
These usually abide by program correctness: show that the program is sound and complete. 
## Examples

### Discussion Example

You are given $2^s$ many arrays of sorted int, each with size $n$. We want to combine them into large sorted array in $O(s2^sn)$
Algorithm: 2nd half of mergeSort. Take the lowest level of the mergeSort tree and merge upwards. 

### CountSort

Recursion:
$C(n)=2C(\frac{n}{2})+2n$
Note: mergeCount is $O(2n)$. 

The cost sum is $\sum_{i=0}^k2^i2n/2^i$. $2n$ can be factored out, and the geometric series can be recalculated for $2nk+k$, where $k$ is $2\log n+1$, so the algorithm is $O(n\log n)$. 
#Algorithms #CS577 #UWMadison #CountSort

Use recursion to split a problem into smaller sub-problems. Typically used 
## Examples

### CountSort

Recursion:
$C(n)=2C(\frac{n}{2})+2n$
Note: mergeCount is $O(2n)$. 

The cost sum is $\sum_{i=0}^k2^i2n/2^i$. $2n$ can be factored out, and the geometric series can be recalculated for $2nk+k$, where $k$ is $2\log n+1$, so the algorithm is $O(n\log n)$. 
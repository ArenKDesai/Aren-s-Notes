#CS577 #Algorithms #UWMadison 

### Quick Select and Sort
Recap of [[Divide and Conquer]]
Problem: Find the $k^{th}$ sorted item in an unsorted list. We would chose a pivot and move all items into partitions accordingly. 
This can be converted into a sorting algorithm by recursively calling quickselect on every partition. 
QuickSort is $O(n)$ . Worst case QuickSort is $T(n) \leq T(n-1)+T(0)+O(n)=O(n^2)$. Best case is $T(n) \leq 2T(n/2)+O(n)=O(n\log n)$. 

## Randomization
Average case analysis: input is drawn from a distribution $\pi$. There are parameters from $\pi$. 
Non-Deterministic algorithms simultaneously consider multiple algorithms weighted by the probability distribution. 
Monte Carlo algorithm returns a $p$ value through brute-force approximation guarantee (run a simulation a lot of times). 
Las Vegas algorithms always return the correct solution or return failure. Expectation is polynomial time. 
Atlantic City algorithms are a combination of the two. 

Random algorithms return a solution 
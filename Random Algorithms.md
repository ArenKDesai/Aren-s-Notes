#CS577 #Algorithms #UWMadison 

### Quick Select and Sort
Recap of [[Divide and Conquer]]
Problem: Find the $k^{th}$ sorted item in an unsorted list. We would chose a pivot and move all items into partitions accordingly. 
This can be converted into a sorting algorithm by recursively calling quickselect on every partition. 
QuickSort is $O(n)$ . Worst case QuickSort is $T(n) \leq T(n-1)+T(0)+O(n)=O(n^2)$. Best case is $T(n) \leq 2T(n/2)+O(n)=O(n\log n)$. 


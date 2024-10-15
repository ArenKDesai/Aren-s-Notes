#CS577 #DynamicProgramming #Algorithms 

Linear programming that calculates solutions from "small" to "large". 

## Weighted Scheduling

Problem: scheduling with compatible schedules, but the schedules are weighted. The [[Greedy]] approach doesn't work since the weights could be higher for one schedule instead of two. 

Dynamic (Recursive) Solution:
$\sigma$ is the set of schedules. Assume $\sigma$ is ordered by finish time. Find the optimal value in sorted $\sigma$ of first $j$ items:
	Find largest $i < j$ s.t. $f_i \leq s_j$. 
	$OPT(j)=\max(OPT(j-1))
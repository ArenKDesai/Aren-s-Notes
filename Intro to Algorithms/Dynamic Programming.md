#CS577 #DynamicProgramming #Algorithms #IntervalScheduling 

"Linear" programming that calculates solutions from "small" to "large". 
On a problem, generate a solution that utilizes "memoization" through:
1. Calculate once; store the value in an array for future calls
2. Can be iterative or recursive

Basic DP Outline:
- Preprocess data
- Populate matrix:
	- Iterate over cells in correct order
	- Understand the work done per cell
Guidelines
- Only polynomial num of subproblems
- Natural ordering of subproblems for enumeration
- Have to be able to calculate larger problems from smaller problems

## Weighted Scheduling

Problem: scheduling with compatible schedules, but the schedules are weighted. The [[Greedy]] approach doesn't work since the weights could be higher for one schedule instead of two. 

Dynamic (Recursive) Solution:
$\sigma$ is the set of schedules. 

**WeightIntDP**
Sort $\sigma$ by finish time.
$m[0]:=0$
for $j=1$ to $n$ do:
	Find index $i$
	$m[j]=\max(m[j-1],m[i]+v_i)$
end

## Longest Increasing Subsequence
Given: int array $A$
Goal: Find longest increasing subsequence. Make sure for $i$, a sequence of indexes, $A[i_k]<A[i_{k+1}]$ for all 
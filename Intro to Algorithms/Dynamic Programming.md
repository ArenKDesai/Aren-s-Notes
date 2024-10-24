#CS577 #DynamicProgramming #Algorithms #IntervalScheduling #GameTheory

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
Use a solution matrix for solved subproblems, the dimension of which usually matches the number of distinct parameters. DP solutions refactor algorithms, not create them. 

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
Goal: Find longest increasing subsequence. Make sure for $i$, a sequence of indexes, $A[i_k]<A[i_{k+1}]$ for all $k$. 
**Subsequence:**
For a sequence $A$, a subsequence $S$ is a subset of $A$ that maintains same relative order. 

Recursive Algorithm: LIS
Input: Integer $k$, and array of integers $A$
Output: Return length of LIS where every value > $k$. 
if $n=0$ then return 0
else if $A[1] \leq k$ then
	return $LIS(k,A[2...n])$
else
	$skip:=LIS(k,A[2...n])$ //*$A[1]$ is not in subsequence*
	$take:=LIS(A[1],A[2...n])+1$ //*$A[1]$ is in subsequence*
	return $\max\{skip,take\}$
end

Start with $LIS(-\infty,A)$, ends with $O(2^n)$ runtime and $O(n^2)$ distinct calls. 

Dynamic solution matrix:
2D array $L$, where $L[i,j]$ is the maximum LIS of $A[j...n]$ with every item $>A[i],i<j$.

Bellman Equation:
$L[i,j]$=
- 0 if $j>n$
- $L[i,j+1]$ if $A[i]\geq A[j]$
- $\max\{L[i,j+1],L[j,j+1]+1\}$ otherwise
	- ^ *skip*,       ^ *take*

Solution in $L[0][1]$; add $A[0]=-\infty$
Populate $j$ from $n$ to 1; $i$ from 0 to $j-1$ or $j-1$ to 0. 

# Dynamic Programming for Games

We typically assume players are rational. 

## Coins in a line

Two players. There are $n$ (even) coins in a line, each with a value. Starting with player A, each player picks a coin from the start or end. Then Player 2 picks a coin from the start or end. Player with the max value wins. 

Greedy Heuristics:
- Largest coin is not optimal.
- Even or Odd Largest Coin wins, but is not optimal. 

Natural dichotomy: Head or tail (start or end, not face of coin)
For Player A's $k$th turn:
	Coin array: $C[i...j]$
	$\max\{c[i]+BOpt(c[i+1...j]),c[j]+BOpt(c[i...j-1])\}$
	               ^ *head*                             ^ *tail*
$BOpt(c[i...j]):=$
	$\min\{AOpt(c[i+1...j]),AOpt(c[i...j])\}$

## Shortest Path
Given a directed weighted graph with no negative cycles, what is the shortest path from $s$ to every other node?
Note: Dijkstra's doesn't give the optimal path. 

We also can't just normalize a graph from the smallest edge as paths with more edges would be impacted more than paths with less edges. 

We start with a 2D matrix $M$ of # of edges in path $\times$ vertices. 
We try to fill out $M$ with $M[i][v]$ being the shortest path from $v$ to $t$ using $\leq i$ edges. However, we need to flip the direction of all the edges, then run this algorithm. 

$M[i][v]=\min(M[i-1][v],\min_{w\in V}(M[i-1][w]+c_{vw}))$

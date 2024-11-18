#CS577 #UWMadison #Interactibility #Algorithms 

Intractability is defining problems that can be solved in polynomial (P) vs non-polynomial (NP) time. In other words, easy vs hard. 
NP problems are categorized in NP-hard and NP-complete. 

Most of the previous algos problems have been optimization problems. We will now analyze decision problems, where there is a binary yes/no answer. For example:
Given a bipartite graph $G$, 
*Optimization*: Find the largest matching. 
*Decision*: Is there a matching of size $\geq k$?
If we know we can solve the optimization problem, we can solve the decision problem. This is reversible (if you run the decision problem many times on a linear or binary search). 
Thus, we can go between optimization problems and decision problems without worrying if one implies the other. 

## Polynomial Time Reductions
Formal notation: $Y\leq_p X$.

Goal: we want an algorithm that can encode any instance of $Y$ into *an* instance of $X$. This can be done if we have a black box solver for $X$. 
Run an instance in Y through a reduction, it outputs a sub-instance in X. The idea is to have a **black box solver for X** that gives us a solution for the sub-instance in X, and that implies a solution for the instance in Y. 
In other words, $I\in Y => I' \in X$, and $solution(I') => solution(I)$. 
There can be multiple instances in X to solve for the instance in Y, but we will focus on 1-1 solutions. 

The reduction solution must cover every possible instance of Y, but does not need to cover every instance of X. 

X is at least as hard as Y. This contrapositive can prove that Y can or can't be solved in polynomial time. 

Vertex Cover $\in$ Set Cover
Independent Set $\in$ Set Packing
### Min Vertex Cover (from Max Independent Set)
if no two nodes in $S$ contain an edge, S is independent. 
If every edge is incident to at least one node in $S$, $S$ has a vertex cover. 
Given a graph $G$ and a number $k$, does $G$ contain an independent set of size $\geq k$? 

The nodes that aren't selected for an independent set form the vertex cover. 
Proof: If $S$ is an independent set, then for any edge, at most one of the two endpoints belong to $S$ (def of independent set), so everything else left over have to contain at least one of the two endpoints. 

From the above theorem, if we find the max independent set, the complement would be the minimum vertex cover. 

### Set Cover (SC)
You have a universe $U$ of elements. There are $m$ subsets $S_m$ in $U$, and we want to find a collection of at most $k$ of the subsets whose unions equal $U$. 

Theorem: $VC \leq_p SC$. 
Proof: we assume a black box solver for SC. $VC=G=(V,E)$. For each vertex, create a set consisting of each edge incident to $v$. This creates a direct correspondence between VC and SC.

This is a generalization of vertex cover. 

### Set Packing (SP)
Same universe as above. Does there exist a collection of at least $k$ subsets that don't intersect?

### Satisfiability Problem (SAT)
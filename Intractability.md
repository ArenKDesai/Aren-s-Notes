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

Run an instance in Y through a reduction, it outputs a sub-instance in X. The idea is to have a *black box solver* for X that gives us a solution for the sub-instance in X, and that implies a solution for the instance in Y. 
In other words, $I\in Y => I' \in X$, and $solution(I') => solution(I)$. 
There can be multiple instances in X to solve for the instance in Y, but we will focus on 1-1 solutions. 

The reduction solution must cover every possible instance of Y, but does not need to cover every instance of X. 

X is at least as hard as Y. This contrapositive can prove that Y can or can't be solved in polynomial time. 

### Independent Set <=> Vertex Cover
if no two nodes in $S$ contain an edge, 
Given a graph $G$ and a number $k$, does $G$ contain an independent set of size $\geq k$? 
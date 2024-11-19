#CS577 #UWMadison #Interactibility #Algorithms #PvsNP

Intractability is defining problems that can be solved in polynomial (P) vs non-deterministic polynomial (NP) time. In other words, easy vs hard. 
NP problems are categorized in NP-hard and NP-complete. 

Most of the previous algos problems have been optimization problems. We will now analyze decision problems, where there is a binary yes/no answer. For example:
Given a bipartite graph $G$, 
*Optimization*: Find the largest matching. 
*Decision*: Is there a matching of size $\geq k$?
If we know we can solve the optimization problem, we can solve the decision problem. This is reversible (if you run the decision problem many times on a linear or binary search). 
Thus, we can go between optimization problems and decision problems without worrying if one implies the other. 

# P
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
We have a set of boolean terms & literals $X:x_1,...,x_n$. $x_i$ is the variable, $\bar{x_i}$ is the negation. 
A clause $C_j$ is the disjunction of terms. A collection / conjunction $C$ is a group of clauses $C_1,...,C_n$. 
The truth assignment function $v:X \to \{0,1\}$ assigns values to terms and returns the conjunction. 
$v$ is a *satisfying assignment* if $C$ is 1, or all $C_i$ evaluate to 1. 

#### Three Satisfiability Problem (3SAT)
Every clause will have 3 distinct literals. 
*Gadgets* are used to show $Y \leq_p X$.

We can **reduce 3SAT to Independent Set (IS)**. Proof:
Assume we have black-box solver for IS. We can transfer any 3SAT to IS through the clause gadget, a $k_3$ graph invented for any clause. If we have $k$ clauses, we'll have $k$ $k_3$ graphs. Out of a $k_3$ graph, we can take one node for an independent set. Thus, the max independent set is $k$. In other words, if we can find an independent set of size $k$, if we use the independent set for solving the literals (where making an edge = True), it necessarily solves the 3SAT. 
However, sometimes we have $\bar{x}$ and $x$ in two clauses. In order to avoid choosing both nodes in the $k_3$ graphs, we can create an edge between the two. 

## Reduction Transitivity
Reductions are transitive. This means that if $Z \leq_p Y$ and $Y \leq_p X$, then $Z\leq_p X$. This also means that:
1. 3SAT $\leq_p$ IS $\leq_p$ VC $\leq_p$ SC
2. 3SAT $\leq_p$ IS $\leq_p$ SP
3. VC $\leq_p$ IS $\leq_p$ SP

# NP
Non-deterministic Polynomial.
A deterministic algorithm is an algorithm where the execution path is completely determined by the input. Non-determinism allows for exploring multiple execution paths simultaneously, similar to randomness. 

Generally, for NP problems, you need to show there exists an efficient certifier for those problems. This can be done by just proving that an algorithm can be verified in polynomial time. 
## Efficient Certification
This is an algorithm that checks if a solution exists in polynomial time. 

For a problem instance, let $s$ be a binary string that encodes the input. $|s|$ is the length of $s$, such as the number of bits in $s$. 
Algorithm $A$ has a P runtime if there is a polynomial time algorithm to solve it. 

Certifier $B(s,t)$ for a problem $P$:
- $s$ in an input instance of $P$.
- $t$ is a certificate, a proof that $s$ is a yes-instance. 
- Efficient:
	- if the input is a yes-instance, for it to be a valid certifier, there must be a certificate that will make the algorithm return a yes-instance. 

### Proving IS $\in$ NP
We define an efficient Certifier $B(s,t)$ which is a set of nodes $i$ ($|V|$ length), where if a node / element is set to 1, it means that node is a part of the set. Two steps:
1. Verify that $|I| \geq k$
2. Verify that $\forall u, v \in I, \forall (u,v) \in E$

#### Million Dollar Question
Is P a proper subset of NP, or is P == NP?

## NP-Hard
Problem $X$ is NP-Hard if for all $Y \in$ NP, $Y \leq_p X$. If we have $X$ that every single NP problem can be reduced to, that is an NP-Hard problem. $X$ may or may not be in NP. 
Problem $X$ is NP-Complete if for all $Y \in$ NP, $Y\leq_p X$, and $X$ is in NP. 
In other words, NP problems that can be reduced to polynomial time. 

NP-Hard problems **do not** need to be NP. 

## NP-Complete
Show that:
1. Problem is NP
2. Problem is NP-Hard
First part is easy --- show that a certifier can be found in polynomial time.
Second part:
1. Prove $X \in$ NP 
2. Start with known NP-Complete problem, reduce it to current problem. 

### CSAT (circuit satisfiability)
3 types of gates - and, or, not. 
Circuit $k$ is a DAG. The source is nodes with no incoming edges. Every other node has a gate. Output: result of the node with no outgoing edges. 
This CSAT problem is NP-Complete. 
Proof:
1. Show that CSAT $\in$ NP (show certificate)
2. We can map from the certifier to CSAT by encoding the certifier as a DAG, where sources: $|s|+|t|=n+poly(n)$ bits. 
3. We can show that we can take any algorithm and reduce it to a CSAT problem (proof omitted). 

We use Karp reduction: Provide an efficient reduction, and show via double imples that $s_y$ is equivalent to $s_x$. 

## 3SAT
We'll show that 3SAT is NP-Complete. 

We can use a truth assignment of the literals as a certificate. A clause can be evaluated in constant time, so SAT formula can be evaluated in
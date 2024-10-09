#CS577 #UWMadison #Algorithms #IntervalScheduling #Dijkstras #Paging

Greedy algorithms choose a locally optimal heuristic, or a metric to work towards minimizing or maximizing by choosing short-sighted optimal actions. 
Greedy algorithms are often not optimal, but are easy to produce. 

There are two main ways to prove a greedy algorithm. 
*Always Stays Ahead*: Establish $S=\langle i_1,...,i_k\rangle$ such that $f_{i_u}<f_{i_v}$ for $u<v$ and $S^*=\langle j_1,...,j_m\rangle$ such that $f_{j_u}<f_{j_v}$ for $u<v$. Prove for all $i_r,j_r$ with $r\leq k$, we have $f_{i_r}\leq f_{j_r}$. 
*Exchange Argument*: Let $S^*$ be an optimal solution. Is it sufficient to show that $|S|=|S^*|$? No. Can there be multiple $S^*$? Yes. We need to show either $S=S^*$, or $S \equiv S^*$ for max lateness. We start with an optimal solution $S^*$ and transform it over a series of steps to something equivalent to $S$ while maintaining optimality. $S^*\equiv S_1\equiv S_2\equiv ...\equiv S$.

## Examples

### Interval Scheduling

Requests: $\sigma=\{r_1,...,r_n\}$
A request $r_i=(s_i,f_i)$, where $s_i$ is the start time and $f_i$ is the finish time. 
Objective: Produce a compatible schedule $S$ that has maximum cardinality. 
Compatible schedule: $S$: $\forall r_i,r_j \in S,f_i\leq s_j \vee f_i\leq s_i$.

Optimal greedy heuristic: Finish First (schedules that end earliest as possible)
Pseudocode (O($n\log n$)):

Let $S$ be an initially empty set.
While $\sigma$ is not empty, do:
	Choose $r_i \in \sigma$ with the smallest finish time (break ties arbitrarily).
	Add $r_i$ to $S$.
	Remove all incompatible requests in $\sigma$. 
end
return $S$. 

Proving optimality:

Let $S^*$ be an optimal solution. We can show the strong claim that $S=S^*$. There can be multiple $S^*$, so we can show the weaker claim of $|S|=|S^*|$. We will use *Always Stays Ahead*. 
By way of contradiction, assume that $|S^*|>|S|$. This implies that $m>k$. FinishFirst is ahead for all $k$ requests. this means it would be able to add the $k+1)-st item of $S^*$. As it did not, this contradicts the definition of FinishFirst. 

### Minimize Max Lateness
$n$ jobs and a single machine that can process one job at a time. 
For job $i$, $t_i$ is the processing time, $d_i$ is the deadline, and lateness $l_i=f_i-d_i$ if finish time $f_i>d_i$; 0 otherwise. 
Objective: Build a schedule for all jobs that minimizes max lateness. 

Optimal greedy heuristic: Earliest deadline first. 

Pseudocode:

Let $J$ be the set of jobs. 
Let $S$ be an initially empty list. 
While $J$ is not empty, do:
	Choose $j\in J$ with the smallest $d_i$ (break times arbitrarily).
	Append $j$ to $S$.
end
return $S$

### Shortest Path

We have a directed graph $G=(V,E)$, where $|V|=n$ and $|E|=m$ and a node $s$ that has a path to every other node in $V$. For each edge $e,\ell_e\geq0$ is the length of the edge. We want to find the shortest path from $s$ to each other node. 

Dijkstra's

Let $S$ be the set of explored nodes. 
For each $u\in S$, we store a distance value $d(u)$.
Initialize $S=\{s\}$ and $d(s)=0$. 
While $S\neq V$, do:
	Choose $v\notin S$ with at least one incoming edge originating from a node in $S$ with the smallest $d'(v)=\min_{e=(u,v):i\in S}\{d(u)+\ell_e\}$. 
	Append $v$ to $S$ and define $d(v)=d'(v)$. 
end

### Paging
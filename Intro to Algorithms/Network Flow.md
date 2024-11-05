#CS577 #UWMadison #Algorithms 

Basic Flow Network:
- Directed Graph $G$
- Each edge $e$ has $c_e\geq0$
- Source $s \in V$ and sink $t \in V$
- Internal node $V /(s,t)$

Defining flow:
- Flow starts at $s$ and exits at $t$.
- Flow function: $f$ : $E \to R^+;f(e)$ is the flow across edge $e$
- Conditions
	- Capacity
	- Conservation
- So the flow incoming must be the exact same as flow outgoing; no change in flow. 
- Flow value $v(f)=f^{out}(s)=f^{in}(t)$

## Maximum-Flow Problem

with flow network $G$, what is maximum flow (max $v(f)$)?
Or, what is the minimum cut?
- A Cut: partition of $V$ into sets $(A,B)$ with $s \in A$ and $t \in B$. Flow form $s$ to $t$ must cross the set $A$ to $B$. 
- Cut capacity: $c(A,B)=\sum_{e}$

Max flow = min cut,  so finding the minimum cut finds the maximum possible flow. 

### Greedy approach for solving
- Initialize $f(e)=0$ for all edges
- While there is a path from $s$ to $t$ with available capacity, push flow equal to the minimum available capacity along path. 

We create a *Residual Graph*, or a graph with all the same nodes as the original graph, but for each edge in the original, you create two edges with $c_e-f(e)$ and $f(e)$. The path that goes from $s$ to $t$ is called the *Augmenting Path*. The augmenting path represents the unused capacity of the graph, typically found through breadth-first search. 

### Ford-Fulkerson Method
Initialize $f(e)=0$ for all edges. Repeat creating residual graphs until there are no augmenting paths left. 

How do we choose an augmenting path? We want to choose paths with large bottlenecks, so we perform the *Scaled Ford-Fulkerson Method*.

Steps:
1. Find a path
2. compute the bottleneck
3. augment path

## Edge-Disjoint Paths

Problem: We have a graph $G$ with $s,t$, and we want the number of edge disjoint paths from $s\to t$. There can be overlapping paths, but no shared edges. 

Directed version: add capacity of 1 to every edge. 
Undirected version: each edge gets converted into two directed edges. Apply directed graph transformation. 

**Observation**: if there are $k$ edge-disjoint paths in 
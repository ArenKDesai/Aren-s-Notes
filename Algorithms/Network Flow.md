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

## Bipartite Matching
Separate the problem into two layers. Set up one source node to one layer, and a sink node to the other. Then, configure the capacities of the source-layer edges, layer-sink edges, and layer-layer edges. For example, a capacity of (0,1) on the source-layer edges can represent choosing one pair matching. 

## Edge-Disjoint Paths

Problem: We have a graph $G$ with $s,t$, and we want the number of edge disjoint paths from $s\to t$. There can be overlapping paths, but no shared edges. 

Directed version: add capacity of 1 to every edge. 
Undirected version: each edge gets converted into two directed edges. Apply directed graph transformation. 

**Observation**: if there are $k$ edge-disjoint paths in $G$ from $s\to t$, then max flow is $k$ in $G'$. 
FF will be $O(mC)=O(mn)$. 

We can recover $k$ edge-disjoint paths through DFS from $s$ to $f$. We set flow to 0 along $P$, the previous path we found, so we don't continuously follow the same path. 

## Image Segmentation

Input $P$ is a set of pixels (image). Separate them into two sets $A,B$, for foreground and background pixels. $a_i>=0$ is the likelihood (not probability) of $i$ being in the foreground. $b_i$ is the same for background. For each adjacent pixel $j$, $p_{ij}=p_{ji}$ is a separation penalty when $i$ and $j$ are not both in $A$ or $B$. 

Goal: Maximize $q(A,B)=\sum_{i\in A}a_i+\sum_{j\in B}-\sum_{i,j\in P:|A \bigcap (i,j)|=1}p_{ij}$

We can implement a min-cut approach to solve this. Every pixel becomes a node, and the penalty becomes the edges. We'll add a source $s$ and connect it to all nodes $i$ with capacity (likelihood) $a_i$. Same with $t$ and all nodes $i$ with capacity $b_i$. 

Run the min-cut on these edges, then use DFS or BFS on the residual graph. 

## Circulation Problems

Now, each node has a demand $d_v$. If the demand is negative, the flow in - flow out is the demand. If demand is 0, then flow in - flow out = 0. Finally, if demand is positive, then flow in - flow out = demand. 
$S$ and $T$ are the sets of sinks and sources. 
Capacity: for each $e\in E, 0 \leq f(e) \leq c_e$. 
Conservation: for each vertex, flow in - flow out is demand. 

**Observation**: If there is a feasible flow, then $\sum_{v \in V}d_v=0$. Also, $D=\sum_{v:d_v>0\in V}d_v=\sum_{v:d_v>0\in V}-d_v$. This is not an iff though. 

Any problem that can be solved with circulation extension can also be solved with regular network flow with more difficulty. 

## Project Selection

Set of projects $P$ with benefits $p_i$ (could be negative). Some projects rely on other projects being completed. 
We use min cut. In general, if you're trying to identify a subset of a graph, use min cut. 
Connect all positive projects to a source, and all negative projects to a sink. Cut the edges between the source and the beginning projects. 

Proof:
We know the min cut will create a set of jobs that is feasible due to the capacity on the edges. This means $c(A', B')=C-\sum_{i\in A}p_i$, which minimizes the cut which maximizes the profit. 

## Min Cost
We have a graph with units per edge, but costs per unit of flow on an edge. We are going to find maximum flow graphs, but now we want to select the minimum cost from those maximum flows. 

### [[Greedy]] Approach
Initialize $f(e)=0$ for all edges, find augmenting edges, and update flow with the bottleneck along $P$ (augmenting path). We use Bellman Ford (although it's slower than Dijkstra's). This is because we know there won't be negative cycles. 
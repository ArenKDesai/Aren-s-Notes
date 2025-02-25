#Graphs #CS240 #UWMadison

[[Relations]] for partial ordering and order relations
## Graph Lemmas
- $\sum_v deg(v) = 2|E|$ 
	- In English, the number of edges in a graph is equal to the sum of the degrees of all the vertices in the graph

### Topological Ordering
[[Relations]] for total order
The topological ordering of a graph is a total order of $\le$

### Simple Paths
A simple path is a path from two vertices where each edge only appears at most once. The start vertex can be visited at the end, making it a **simple cycle**.

### Trees
A connected acyclic undirected graph. 

### Transitive Closure
The set of all vertices reachable by another vertex. For example, while a graph may contain edges (x,y) and (y,z), the transitive closure of that graph will contain (x,z). 
A list of all the ordered pairs in the transitive closure of a graph will contain the vertices themselves, so a simple graph of vertices x,y and edge x->y will have 3 ordered pairs.
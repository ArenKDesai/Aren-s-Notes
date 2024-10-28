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

## Maximum Matches

With a set of nodes and edges (not neccessarily connected), find the maximum pairs. 
We can redefine this as a network flow problem by positioning the nodes as two arrays of nodes, and creating "flows" through the existing edges. We're only gonna do this with bipartite graphs. 

## Maximize Skills, Minimize Course Cost
Classes cost $c_i$, give you $v_i$ value, and lead into eachother in order to gain $v_i$. We cannot define this as $\max(u-c)$ since we can't have negative flow, so we try to minimize
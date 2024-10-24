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

/w flow network $G$, what is maximum flow (max $v(f)$)?
Or, what is the minimum cut?
- A Cut: partition of $V$ into sets $(A,B)$ with $s \in A$ and $t \in B$. Flow form $s$ to $t$ must cross the set $A$ to $B$. 
- Cut capacity: $c(A)
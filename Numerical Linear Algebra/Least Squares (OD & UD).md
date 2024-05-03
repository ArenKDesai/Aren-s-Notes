#CS513 #LinearAlgebra #ML #UWMadison 

Given: $Ax=b$
$x^* \in R^m$ is a least squares solution if $||Ax^*-b||_2 \le ||Ax-b||_2, \forall x \in R^m$
# Overdetermined LS
No exact solution = Overdetermined
In the space $V = R^m$, we have $v=b$. We also have $W \in V$, where W is the range of A. We want to find $w^* \in W$ such that $||w^*-v||_2 \le ||w-v||_2, \forall w \in W$ 
With V and W, assume $\tilde{w} \in W$, which satisfies $v-\tilde{w} \perp W$. $\tilde{w}$ is the only LS solution. 

### Normal Equation
$A'Ax^*=A'b$
This will always work. However, cond(A'A) = cond(A)^2. 

### QR-Factorization Approach
[[QR Factorization]]
Steps:
1. $A=QR$
2. $Rx=Q'b$
cond(Q'A) = cond(A)

Assume $A_{mxm}$ and $B_{mxm}$, as well as range(A)=range(B). Then, $Ax^*=By^*$.
Also, $B'Ax=B'b$, and $A'By=A'b$. 
Finally, $Ax^*=Q_1Q_1'b$. 
# Underdetermined LS
Multiple solutions. Assume $A'x=b$. Best solution = $x^*$.
If $y \in R^n$ such that $A'y=b$ and $y \perp ker(A')$, then $y=x^*$.

## Algorithm
1. $A'x=b$
2. $A=QR$
3. $R't=b$
4. $x^*=Qt$
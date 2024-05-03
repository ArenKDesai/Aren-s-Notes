#CS513 #Condition #Stability #LinearAlgebra 

## Setup
We have two equations:
1. $Ax=b_0$, $x_0=A^{-1}b_0$
2. $Ax=b_1$, $x_1=A^{-1}b_1$
We want to find the ratio $\frac{||b_0||}{||b_1||}$.
This ratio cause linear systems to have errors in finite precision environments. 

### Condition Number
cond(A) = $\frac{max(||Av||:||v||=1)}{min(||Av||:||v||=1)}$
If A is square and invertible, then
cond(A) = $||A||||A^{-1}||$
If A is orthogonal, then
cond(A) = 1

# Stability
When factoring $A \to BC$, it is possible that cond(A) << cond(B)cond(C). This would mean that the system is unstable. 

If $A=QR$, then cond(A) = cond(R), and cond(Q) = 1. [[QR Factorization]], then, is very stable. 
#LinearAlgebra #CS513 #UWMadison #PowerMethod

We want to approximate eigenvectors. This means we want to maximize the equation $\lambda v=w, w=Av$
This can be solved as an overdetermined equation [[Least Squares (OD & UD)]]. 

## Raleigh-Riesz Quotient
- Input: $A_{mxm}, v$
- Output: approx. eigenpair
$v\lambda =w, w=Av$
$\lambda = \frac{(v,Av)}{(v,v)}$
We have $A_{mxm},(v_k)_k$ as a series of vectors, and we want to know if it converges to an eigenvector. 
1. Add approx e-val $\lambda_k$ to each $v_k$
2. $\alpha_k=\frac{||Av_k-\lambda_kv_k||}{||Av_k||}$ (which should converge to 0)

# Power Method
We want to find an eigenpair of A. 
- Input: $v_0$
1. $v_k=Av_{k-1}$
	1. If A is diagonalizable, the power method converges to a dominant pair, which means $|\lambda| \ge |\mu|, \forall \mu \in \sigma(A)$
	2. 
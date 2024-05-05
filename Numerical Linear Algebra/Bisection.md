#UWMadison #LinearAlgebra #CS513 

Goal: find $\sigma(A)$ given A
- Input: $I$, with $n$ eigenvalues.

1. $A=A'$
2. $A=LDU$
or
1. $A=A-sI$
2. $A=LDU$

[[Linear Algebra Misc]] for info on main principle minors
### Theorem
$A_{mxm}$
$d_0=1,d_1,...,d_m=det(A)$
Inertia of A = $\#\{1 \le k \le m : d_{k-1} d_k > 0\}$

### Algo 2
1. $A=A-sI$
2. $d_k=d_k(A_s), k=0,...,m$
3. $\#_s$ is the number of sign changes

If you want to compute the main principle minor of a tridiagonal hessenberg S,
1. $d_0(S)=1,d_1(S)=S(1,1)$
2. $d_k(S)=S(k,k)d_{k-1}(S)-S(k,k-1)S(k-1,k)d_{k-2}(S), k=2,3,...$
$O(m)$


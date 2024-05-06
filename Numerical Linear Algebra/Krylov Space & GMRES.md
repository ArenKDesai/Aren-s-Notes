#LinearAlgebra #UWMadison #CS513 

# Krylov Space


# GMRES
Given: $Ax=b$, exact solution $x^*$, we form $K_n=span{b,Ab,...,A^{n-1}b}$. We define $x_n \in K_n$ as the least squares performer: $x_n \in K_n$ and $||Ax_n-b||_2 \le ||Ax-b||, \forall x\in K_n$ 
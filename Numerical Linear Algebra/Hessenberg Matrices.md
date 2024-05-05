#UWMadison #LinearAlgebra #Hessenberg

Matrices that are upper triangular with one more layer of values below the diagonal. Useful for quickly computing eigenpairs. Conversion is $O(m^3)$, eigenpair query is $O(m)$. 

(for details on householder matrices, see [[QR Factorization]])
- Input: $A$
1. $S_0=A$
2. $x=S_0(:,1)$
3. $y=\begin{bmatrix}x(1) \\ ||x(2:m)|| \\ 0 \\ . \\ . \\0 \end{bmatrix}$
4. $w_1=(x-y)/||x-y||$
5. $S_1e_1=(H_1(S_0(H_1e_1)))=(H_1(S_0e_1))=H_1x=y$

## General Step
- $x=S_{j-1}(:,j)$
- $y=\begin{bmatrix} x(1)\\.\\.\\x(j)\\||x(j+1:m)||\\0\\.\\.\\0 \end{bmatrix}$
- $w_j=(x-y)/norm(x-y)$
- $S_je_i=(H_j(S_{j-1}(H_je_i)))=(H_j(S_{j-1}e_i))$


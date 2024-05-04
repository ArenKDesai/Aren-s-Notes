#CS513 #UWMadison #LinearAlgebra 

- Input: $A_{mxm}$
- Output: $LU$
	- L is lower triangular
	- U is upper triangular

## Algorithm
Same as [[QR Factorization]], $A=A_0$, $A_0 \to A_1 \to ... \to A_{m-1}=U$
Where $A_j=L_jA_{j-1}$
And $U=L_{m-1}L_{m-2}...L_1A$
And $L=L_{1,v_1}^{-1} ... L^{-1}_{m-1,v_{m-1}}$
$L(i,j)=v_j(i),i>j$

## Step One
- Input: $A_0=A$
- Output: $v_1$
	- $v_1(1)=0$
	- $A_1=(I-v_1e_1')A$
1. $v_1=A(2:m,1)/A(1,1)$
2. $L(2:m,1)=v_1$

## Step Two
- Input: $A_1$
- Output: $v_2$
	- $A_2=(I-v_2e_2')A_1$
1. $v_2=A(3:m,2)/A(2,2)$
2. $L(3:m,2)=v_2$

## Complexity
$\frac{m^3}{3}$
If A is invertible, then $A=LU$ is unique. 

### Applications
- LU factoring a matrix can make calculating its determinant an $O(m^3)$ operation. 

### Stability
LU factoring is unstable. However, partial and full pivoting moves the rows and columns to avoid using pivots small relative to other entries. 
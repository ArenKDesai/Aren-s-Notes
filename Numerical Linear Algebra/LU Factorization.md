#CS513 #UWMadison #LinearAlgebra 

- Input: $A_{mxm}$
- Output: $LU$
	- L is lower triangular
	- U is upper triangular

## Algorithm
Same as [[QR Factorization]], $A=A_0$, $A_0 \to A_1 \to ... \to A_{m-1}=U$
Where $A_j=L_jA_{j-1}$
And $U=L_{m-1}L_{m-2}...L_1A$
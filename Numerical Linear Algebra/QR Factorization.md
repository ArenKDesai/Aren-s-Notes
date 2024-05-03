#LinearAlgebra #CS513 #UWMadison #Householder

## Outline
- Input
	- $A_{mxm}$, $\exists A^{-1}$ 
- Output
	- Q, orthogonal
	- R, upper triangular
	- A = QR

## Algorithm
$A_0 \to A_1 \to ... \to A_{m-1}$
$A_0 = A$
Each step through the process, $A$ becomes closer to upper triangular. $A_1$ is upper triangular on the first column only, $A_2$ on the first and second columns, and so on. The last column does not need to be adjusted. 

### Basics
- Input
	- $A_{j-1}$, $1 \le j \le m-1$
- Output
	- $A_j = H_jA_{j-1}$
	- $H_j$ is orthogonal and symmetric
	- $A_{m-1}=H_{m-1}H_{m-2}...H_1A_0$
	- $Q=H_1...H_{m_1}$
	- $A=QR$

### Householder Matrices
- $H_w=I-2ww'$
- $w \in R^m$, $||w||_2=1$
- Properties
	- Symmetric
	- Orthogonal
	- Self-invertible ($H^{-1}=H$)
	- $Hw=-w$
	- If $(v,w)$ then $Hv=v$
	- H can map a certain x to a certain y

## First Step
- Input
	- $A_0=A$
- Output
	- $H_1$
	- $A_1=H_1A_0$

1. $x=A_0e_1$ (first column of A)
2. $y=||x||_2e_1$
3. $w = \frac{x-y}{||x-y||_2}$
4. $H_1=I-2ww'$
5. $A_1=H_1A_0$

## Generic Step
- Input
	- $A_{j-1}$
- Output
	- $A_j$
	- $H_j$, where $A_j=H_jA_{j-1}$

1. $x=A_{j-1}e_j$
2. $y=\sum^{j-1}_{i=1}x(i)e_i+||x(j:m)||_2e_j$
3. $w=(x-y)/||x-y||_2$
4. $H_j=I-2ww'$
5. $A_j=H_jA_{j-1}$
#Statistics #Stat456 #Factorizing #ML #LinearAlgebra 

We have a set of manifest variables, and we want to find a set of (or one) common latent variables. For example, we may have a set of test scores, and we want to find a student's underlying intelligence. This is very similar to [[Principal Component Analysis]]

For all $X$ recorded as data, $X_n=\lambda_nF+U_n$. F is a latent variable / common factor, lambda is a factor loading, and U is error or specific factors. X is the only variable observed. They usually are assumed these attributes:
1. $F$ and $U$ are independent
2. $E(F)$ and $E(U)$ both = 0.
3. $var(F)=1$
4. $var(U)=\psi$
5. $F$s and $U$s are multivariate Gaussians. 

$\sigma_{jj}=\lambda_{j1}^2+\lambda_{j2}^2+...+\lambda_{jk}^2+\psi_j$
^var($X_j$)
$\sum_{j=1}^p\sigma_{jj}=\sum_{l=1}^k\sum_{j=1}^p\lambda_{jl}^2+\sum_{j=1}^p\psi_j$

Model:
$X-\mu=\Lambda F + U$
$\Lambda=\lambda_{pxk} F_k U_p$

## Algorithm
Goal: estimate $\Lambda, \Psi$ by finding a decomposition $S \approx \hat{\Lambda}\hat{\Lambda}'+\hat{\Psi}$
To choose a number of factors, you can use percentage of variance explained, or look at a scree plot. 
Factor loadings are not complete. $\Sigma = \Lambda\Lambda'+\Psi=(\Lambda R)(\Lambda R)'+\Psi$

For factor rotation, factors are uncorrelated, so varimax is used. You have to find an orthonormal $R$ that maximizes square loadings $\frac{1}{p}\sum_{i=1}^k \begin{bmatrix}\sum_{j=1}^pl^4_{ji}-\begin{pmatrix}\sum_j=1^pl_{ji}^2 \end{pmatrix}^2 \end{bmatrix}$ ($L=(l_{ji})_{pxk}=\Lambda R$ is the rotated factor)
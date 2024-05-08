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

One possible method for projecting data onto factor directions is using $\hat{\Lambda}^TS^{-1}x_i$ as the sample estimator and, based on the conditional distribution $F|X=x$, $N(\Lambda^T \Sigma^{-1}x,(\Lambda^T\Psi^{-1}\Lambda+I)^{-1})$

Sum of squares of loadings = $\sum_{j=1}^p \lambda_{jl}^2$
SS loadings of factor $l$ over total variance $\frac{\sum_{j=1}^p \lambda_{jl}^2}{\sum_{j=1}^p \sigma_{jj}}$
sum of SS loadings up to factor $v$ over total variance: $\frac{\sum_{l=1}^v\sum_{j=1}^p \lambda_{jl}^2}{\sum_{j=1}^p \sigma_{jj}}$

Examples
$R=\begin{pmatrix}Classics\\French\\English \end{pmatrix}\begin{pmatrix}1.00\\0.83&&1.00\\0.78&&0.67&&1.00\end{pmatrix}=\begin{pmatrix}\lambda_1\\ \lambda_1\\ \lambda_3 \end{pmatrix}(\lambda_1 \lambda_2 \lambda_3) + \begin{pmatrix}\psi_1&&0&&0\\0&&\psi_2&&0\\0&&0&&\psi_3 \end{pmatrix}$

Unique solution: $\hat{\lambda}_1=0.99, \hat{\lambda}_2=0.84, \hat{\lambda}_3=0.79, \hat{\psi}_1=0.02,\hat{\psi}_2=0.30, \hat{\psi}_3=0.38$
Note: if $\psi$ is negative, then it is not a proper solution. 

While PCA is usually used to explain cumulative variance in minimized dimensions, FA is usually used to explain covariance or correlations through common factors (may or may not be smaller dimension). 
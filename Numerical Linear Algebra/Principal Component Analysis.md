#CS513 #ML #UWMadison #Statistics #LinearAlgebra 

Given: sequence $x_1,...,x_k$ in $R^m$. PCA states that there is a subspace W in $R^m$ of lower dimension that all vectors are sampled from. 

For each x in the sequence, $||x_j-w_j||_2 \le ||x_j-w||_2, w \in W$ 
This establishes $er(j) = ||x_j-w_j||_2$. The score is $\sqrt{\sum^k_{j=1}er(j)^2}$. 

## PCA Theorem
With a large matrix X with columns $(x_j)^k_{j=1}$, we use SVD on X. The optimal subspace $W_n$ is $span\{U(:,1),...,U(:,n)\}$, where U is from the SVD. The score of $W_n$ is $\sqrt{\sum^{min\{m,k\}}_{j=n+1}\sum(j,j)^2}$

### Steps
1. Choose $W=span\{w\},||w||_2=1$. The least squares approx. to $x \in R^m$ from W is $x\approx w_x = (w,x)w$. 
2. $||x||^2_2=||w_x+(x-w_x)||^2=||w_x||^2_2+||x-w_x||^2_2=|(x,w)|^2+||x-w_x||^2_2$
3. $\sum^k_{j=1}|(x_j,2)^2=\sum^k_{j=1}||x_j||^2_2-\sum^k_{j=1}||x_j-w_{x_j}||^2_2$
4. Maximize $\sum^k_{j=1}|(x_j,w)|^2$
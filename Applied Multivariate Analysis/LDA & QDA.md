#Stat456 #Statistics #UWMadison 

An extension of [[Multivariate Gaussian Mixtures]]
# LDA
Assume equal variance ($\sigma_k^2=\sigma^2$ for any $k=1,...,K$)
Compare $P(Y=k|X=x)\propto p_k(x)\pi_k$
For $k \neq j$, we investigate the difference $\delta_k(x)-\delta_j(x)$, where the discriminate function is $\delta_k(x)=x\frac{\mu_k}{\sigma^2}-\frac{\mu_k^2}{2\sigma^2}+log\pi_k$
The classifier / decision rule is $\hat{C}(x)=arg\ max_k\delta_k(x)$
The decision boundary is $\{x:\delta_k(x)-\delta_j(x)=0\}$


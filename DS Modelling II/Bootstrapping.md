#Stat340 #Bootstrapping #Statistics #ML #UWMadison

Resamples data as though it were the population itself (similar to permutation tests in [[Testing]]). This is helpful for situations like estimating the confidence interval for a distribution, where using a Monte Carlo test may be too computationally heavy, but doing the math for the CLT would be too complicated. Or, more importantly, sometimes we don't want to make model assumptions. Bootstrapping is a non-parametric statistic method. 

Steps:
1. Sample with replacement. P.S. $X^*_n$ means that $X_n$ was resampled from the data. 
2. Compute an estimator ([[Estimation]]) on the new sample. 
3. Repeat those two steps B times, and compute test statistic. 
Ex. 
Compute $SE_{boot}=\sqrt{\frac{1}{B} \sum^B_{b=1}(\hat{\theta}_b-\frac{1}{B} \sum^B_{r=1}\hat{\theta}_r)^2}$
Compute the confidence interval $(\hat{\theta}-1.96SE_{boot},\hat{\theta}+1.96SE_{boot})$

However, there are certain challenging functions like maximum and minimum that bootstrapping struggles on, and underestimates the variance of the statistic. Generally speaking, the test statistic has to follow a normal distribution. 
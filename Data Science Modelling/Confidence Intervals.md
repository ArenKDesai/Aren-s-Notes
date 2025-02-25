#Stat340 #Statistics #ConfidenceIntervals #UWMadison

Assume a statistic S ([[Random Variables]]) is a function that estimates $\theta$, and we assume that $\mathbb{E}S=\theta$ ([[Estimation]]). This means our estimator is unbiased for $\theta$. If we know the distribution, we could calculate $\mathbb{E}S=\theta$ directly, but without that knowledge, we need a confidence interval. 

The definition of a confidence interval is a data-dependent interval with the property that when the data are drawn under the distribution with parameter $\theta$, $Pr[\theta \in C(X_1,X_2,...,X_n);\theta]=Pr[L \le \theta \le U]=1-\alpha$. In other words, the interval needs to be random, specifically in the interval C, not S. 

In practice, this means finding an estimated parameter, generating data from the model with that parameter, and computing the statistic S on that data. This will be an approximately correct confidence interval. 

Ex:
```r
data = rpois(80, 2.718) # data that was collected with an uknown lambda
lambda_hat = mean(data)
NMC = 2000
replicates = rep(NA,NMC)
for(i in 1:NMC) {
	fake_data = rpois(length(data), lambda_hat)
	replicates[i] = mean(fake_data)
}
CI = quantile(replicates, probs=c(0.025, 0.975)) # The quantiles for 95% CI
```

### The Central Limit Thereom
If $X_1,X_2,...,X_n$ are i.i.d. random variables with shared mean $\mu=\mathbb{E}X_1$ and variance $\sigma^2=Var(X_1)$, then as $n \to \infty$, the standardized random variable is well approximated by a standard normal ([[Random Variables]]).
With that, we can approximate quantiles for the scaled and centered sample mean, $\frac{\bar{X}-\mu}{\sqrt{\sigma^2/n}}$.
Ex:
```r
data = rpois(100, lambda = 2)
x_bar = mean(data)
var_hat = var(data)
n = length(data)
CI = c(x_bar - 1.96*sqrt(var_hat/n), x_bar + 1.96*sqrt(var_hat/n))
```
#Stat340 #Estimation #Statistics #PointEstimate #LawOfLargeNumbers #UWMadison

When trying to estimate something, you generate a *point estimate*, labeled $\hat{\mu}$. This is usually the mean of a sample $\bar{X}$. This makes sense, as $\hat{\mu}$ is the [[Expectation]] of a sample. 

A test statistic is usually chosen to try to estimate for a sample. The function S is that test statistic (as test statistics are functions), and S is called the *estimator*. [[Testing]] touches more on test statistics. 

The *sampling distribution* is the distribution for how a test statistic may behave. 
If an estimator $\hat{p}$ is equal to the thing we are trying to estimate, it's called an *unbiased estimator*. This is typically seen in $\mathbb{E}S=\theta$

We can use the variance to estimate how close a variable is on average to its expectation. 
$Var(\hat{p})=Var(\sum^n_{i=1}\frac{X_i}{n})$ and X is independent, so $Var(\hat{p})=Var(\sum^n_{i=1}\frac{X_i}{n})$
In conclusion, $Var(\hat{p})=\frac{p(1-p)}{n}$. We will be taking the square root of this in order to get the standard deviation, which is a better measure of how well our point estimate is doing. 

## Law of Large Numbers
- Weak law: if $X_1,X_2,...,X_n$ are i.i.d. (independent and identically distributed) with mean $\mu$, then $lim_{n \to \infty}Pr[(\frac{1}{n}\sum^n_{i=1}-\mu)>\epsilon]=0$. In English, this is saying that as you generate more data points, the point estimate $\hat{\mu}$ becomes a better predictor of the true mean $\mu$. For any fixed $\epsilon > 0$, we can guarantee that the sample mean $\bar{X}$ is within $\epsilon$ of $\mu$ with arbitrarily high probability, so long as our sample size $n$ is long enough. This also extends past the sample mean, and as long as $S$ is constructed in an appropriate way, $S$ will be close to any parameter we want to estimate. 

The method of moments is a technique for doing estimation. It involves estimating a parameter by expressing in moments, like $\mathbb{E}X,\mathbb{E}X^2,\mathbb{E}X^3$
#Stat340 #Testing #Statistics #UWMadison


Basic Outline:
1. Start with a *null hypothesis*: the hypothesis that something was random, or something doesn't have a pattern
2. Organize observations 
3. Collect data
4. Compare data to *null hypothesis*
5. Compare data to $\alpha$, the pre-determined value (usually 0.05) that would signify that the null hypothesis was correct. 

Tool for calculating that data: [[Monte Carlo]]

### Parametric Testing
Assume a parametric model for the data. This is a model where the data is calculated with a random variable distribution and known parameters. 

### Permutation Tests
Take known data and reshuffle it. This is a type of [[Monte Carlo]] test. 

### Errors
- Type I error: an error corresponding to rejecting a null hypothesis when the null hypothesis is true. "False Alarm"
- Type II error: an error corresponding to accepting a null hypothesis when the null hypothesis is false. "Miss"
- The probability that we commit a Type I error is $\alpha$

### One-Sided vs Two-Sided Tests
- A one-sided test may only be able to detect a statistically significantly different value in our response variable if the response variable goes one way. For example, if $y$ is too high, but the test cannot detect if $y$ is too low. 
- Want to find an $\alpha$ that satisfies that the probability of rejecting the null hypothesis is a union of the probability that our test statistic $t$ is significantly too high OR too low. 
- The set where $x:x<t_{\alpha,1}$ or $x>t_{\alpha,1}$ is a rejection region it is the set of values that, when observed, would mean we reject the null hypothesis. 
- When plotting a PMF of a binomial, the $\alpha$ value would be the area under the curve OUTSIDE of the two lines. Inside is $1-\alpha$. 
- We find the upper and lower bound by qbinom(0.025, $\mu$, $p$) and qbinom(0.975, $\mu$, $p$)
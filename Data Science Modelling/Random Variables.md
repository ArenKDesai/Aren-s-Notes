#R #Stat340 #RandomVariables #Distributions #Statistics #UWMadison

Note: Discrete variables have probability mass functions, while continuous variables have probability density functions

Standard error of S = $\frac{\sigma}{\sqrt{n}}$

#### Bernoulli
- Yes or no question, 1 or 0
- discrete
Param:
- p, probability of 1
- q = 1 - p

#### Binomial
- Yes or no with count of trials
- Binomial(n, p)
- discrete
Param:
- n, number of trails (size)
- p, probability of 1

#### Geometric
- Flipping coins, counting until tails
- rgeom(1, prob=0.5)
- discrete
Param:
- p, prob of heads
Prob of certain value:
- Pr\[X=k\] = (1-p)<sup>k</sup>p

#### Poisson
- discrete
Ex:
- Customers arriving to a store on a given day
- calls to a phone line between 2pm and 3pm
- Photons or other particles hitting a detector during an experiment
- cars arriving at an intersection
- $\mathbb{E}X_i=\lambda$
Param:
- $\lambda$, the rate parameter. Larger lambda means more arrivals per unit time (higher rate). Always greater than 0. 
Probability mass function:
- Pr\[X=k] = λ<sup>k</sup>e<sup>-k</sup> / k!

#### Uniform Continuous or Discrete
- Uniform distribution
- Doesn't need parameters other than bounds

#### Normal / Gaussian
- Bell curve
- Standard normal has $\mu = 0, \sigma^2 = 1$.
- Changing $\mu$ changes the center of the bell curve
- Changing $\sigma^2$ changes the height and breadth of the curve
Param:
- mean $\mu$ and variance $\sigma^2 > 0$.

#### Exponential
- Continuous
- Waiting times
- Continuous version of geometric distribution
Param:
- $\lambda$, the rate
- $\mathbb{E}\bar{X}=\frac{1}{\lambda}$

## Example Problems
- $X = norm(\mu=1, \sigma^2=3)$. What is the probability that $0 \le X \le 3$?
- Compute the integral $\int_0^3 \frac{1}{\sqrt{2\pi*3}}$ exp{$\frac{-(t-1)^2}{2*3}$}

### Quantiles
- qnorm, qbinom, etc.
- Takes a probability $p$, and gives the number (quantile) $t$ where the probability that X is less then or equal to $t$ is equal to $p$. 
- Inverse CDF

## Standardizing Random Variables
$\frac{\frac{1}{n}\sum^n_{i=1}X_i-\mu}{\sqrt{\sigma^2/n}}$
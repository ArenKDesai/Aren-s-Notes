#Stat340 #Expectation #Statistics #UWMadison

For odds, see [[Logistic Regression]]
## Expected Value
The expectation of a random variable ([[Random Variables]]) X with outcome set $\Omega$ is $\mathbb{E}X=\int_\Omega tf_X(t)dt$ for continuous with density $f_X$ and $\mathbb{E}X = \sum_{k \in \Omega}kPr[X=k]$ if X is discrete. This may change depending on [[Independence & Conditional Probability]].
Var $X=\mathbb{E}(X-\mathbb{E}X)^2=\mathbb{E}X^2-\mathbb{E}^2X$ or $\mathbb{E}(X^2)-\mu^2$

($\mathbb{E}^2X \equiv (\mathbb{E}X)^2$)
$\mathbb{E}X = \mu$
$\mu$ is a constant, so $\mathbb{E}\mu^2 = \mu^2$

Expectation is linear, so constants do not affect it. $\mathbb{E}(aX+b) = a \mathbb{E} X+b$. This is because constants are non-random. 
However, X and Y are random variables, so $\mathbb{E}(X+Y)=\mathbb{E}X+\mathbb{E}Y$

The expectation of a sum is the sum of expectations ($\mathbb{E}(X_1+X_2+...+X_n)=\mathbb{E}X_1+\mathbb{E}X_2+...+\mathbb{E}X_n$), but the variance of the sum is **not** the sum of variances. 
Var(X+Y) = $\mathbb{E}[X+Y-\mathbb{E}(X+Y)]^2$ or $\mathbb{E}[(X-\mathbb{E}X)+(Y-\mathbb{E}Y)]^2$

[[Independence & Conditional Probability]] continues the idea of expected value with covariance. 
#R #ML #Stat340 #Statistics #Regression #RidgeRegression #ML #LinearRegression #LASSO #UWMadison

Ridge Regression shrinks estimated coefficients toward zero by changing the loss. Take the typical linear regression least squares objective:
$\sum^n_{i=1} (Y_i-\beta_0-\sum^p_{j=1} \beta_j X_{i,j})^2$
and adding the penalty term $\lambda \sum^p_{j=1}\beta^2_j$ where $\lambda$ is a tuning parameter. 

Ridge Regression / Loss function: RSS + lambda * sum(Beta^2) of all predictors
[[Variable Selection]] for RSS

```r
library(MASS)

lambda_vals = c(0,1,2,5,10,20,50,100,200,500)

lm.ridge(RESPONSE_VAR ~ ., DATASET, lambda = lambda_vals)
```

lambda = 0 is equivalent to a simple linear regression

Issue with Ridge Regression: It doesn't reduce the number of coefficients. LASSO does this. 

## LASSO
Same as Ridge, but penalty function now takes the absolute value of the coefficients, not the sum: $\lambda \sum^p_{j=1}|\beta^2_j|$. Cross-Validation ([[Variable Selection]]) can be used to find $\lambda$. 
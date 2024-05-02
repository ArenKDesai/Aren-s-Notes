#Stat340 #Statistics #LogisticRegression #Regression #ML #Odds #UWMadison

When you try to predict a binary variable, such as whether someone has diabetes or not, that calls for a logistic regression. A logistic regression outputs a probability instead of a prediction using the logistic function:
$\sigma(z)=\frac{1}{1+e^{-z}}={\frac{e^z}{1+e^z}}$. This is an example of a sigmoid function. In our case, $z=(\hat{\beta}_0+\hat{\beta}_1 x)$. 

### Multiple Logistic Regression
Same idea as [[Multiple Regression]]. 
$Pr[Y_i=1;X_i=\frac{1}{1+exp(-(\beta_0+\beta_1 x_1+\beta_2 x_2+...+\beta_p x_p))}]$. 
Ex:
```r
log_reg = glm(resp ~ 1 + pred, data=data, family=binomial) # The response variable is binomial. Could also be continuous
predict(log_reg, type='response', newdata=data.frame(pred=300)) # 300 is arbitrary
```

### Odds
Odds of event E with probability p are $Odds(E)=\frac{p}{1-p}$. This is the ratio of the probability of an event happening to the probability of the event not happening. 
This can be extended to logistic regressions, where:
$Odds(x)=\frac{p(x)}{1-p(x)}=\frac{1}{exp(-(\beta_0+\beta_1 x))}=exp(\beta_0+\beta_1x)$
However, the log odds are more commonly used since odds can get very small, so $Log-Odds(x)=\beta_0+\beta_1x$.

Log likelihood function:
$\sum^n_{i=1}y_i log(\frac{1}{1+exp()-(\beta_0+\beta_1x)})+(1-y_i)log(\frac{1}{1+exp(\beta_0+\beta_1x)})$
This is monotone, meaning a large likelihood is the same as a large log likelihood. Our loss function for a logistic regression is thus the negative log likelihood:
$\ell(\beta_0,\beta_1=-\sum^n_{i=1}y_i log(\frac{1}{1+exp()-(\beta_0+\beta_1x)})+(1-y_i)log(\frac{1}{1+exp(\beta_0+\beta_1x)}))$
Choosing parameters to maximize the probability of data is called maximum likelihood estimation. Often, least squares estimate and maximum likelihood estimate are the same. 

### Least Squares and Maximum Likelihood
Choosing a number that minimizes $min_m \sum^n_{i=1}(x_i-m)^2$, which, with some calculus, $m=\frac{1}{n}\sum^n_{i=1}x_i=\hat{\mu}$
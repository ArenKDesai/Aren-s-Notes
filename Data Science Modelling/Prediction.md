#Statistics #Stat340 #Prediction #Regression #LinearRegression #ML #UWMadison

Given data pairs $(X_1,Y_1)(X_2,Y_2)...(X_n,Y_n)$, we use $X_i$ to predict $Y_i$. X is often called an independent variable or a predictor variable, whereas Y is a response variable or dependent variable. 

### Simple Linear Regression
$Y_i=\beta_0+\beta_1X_i+\epsilon_i$
$\beta_0$ is the intercept term, $\beta_1$ is the coefficient associated with a predictor, and $\epsilon_i$ is an error term. For multiple predictors, see [[Multiple Regression]]. The error term measures uncertainty. The error terms are independent, modeled by $\epsilon_i$ ~ $N(0,\sigma^2)$. 
An assumption of linear models are that the residuals are independent and have mean zero. We also usually assume they are normally distributed with mean 0. Additionally, looking at the expected value of a certain point, $\mathbb{E}Y_i$, the error term drops off. 
$\beta_1$ is the change in the response variable for every 1 unit increase in the predictor variable. Be cautious about the intercept term though, when X=0 the intercept term can make no sense. Also, be careful to say that "an increase in X indicates an increase in Y", not "an increase in X causes an increase in Y". 

In R, a simple confidence interval can be generated like so:
```r
confint(lm.model, level=0.95)
```
And a prediction can be made like this:
```r
predict(lm.model, newdata=data.frame(simulated_xi=500)) # 500 is an arbitrarily chosen value
```

## Loss Functions
Takes a choice of model parameters and outputs a number that measures how poorly a model is fitting data. For greater detail, see [[Variable Selection]]. 

### Sum of Squares
Also goes by residual sum of squares (RSS) or sum of squared errors (SSE). The equation is $l(\beta_0,\beta_1)=\sum^n_{i=1}(y_i-\hat{y}_i)^2=\sum^n_{i=1}(y_i-(\beta_0+\beta_1x_i))^2$. The terms $y_i-\hat{y}_i=y_i-(\beta_0+\beta_1x_i)$ are the residuals. These are the left over errors from comparing the real data to the prediction. Minimizing the sum of squared residuals loss is ordinary least squares. 
Note: The sum of squared errors doesn't have to be the loss statistic. For example, the standard deviation could also be used. 
Calculus is used to solve $\frac{\partial \ell(\beta_0,\beta_1)}{\partial \beta_0}=0$ and $\frac{\partial \ell(\beta_0,\beta_1)}{\partial \beta_1}=0$. Our estimates end up being the following:
$\hat{\beta_0}=\bar{y}-\hat{\beta}_1 \bar{x}$
$\hat{\beta}_1=\frac{\sum^n_{i=1}(x_i-\bar{x})(y_i-\bar{y})}{\sum^n_{i=1}(x_i-\bar{x})^2}$
$\bar{x}=\frac{1}{n}\sum^n_{i=1}x_i$ 
$\bar{y}=\frac{1}{n}\sum^n_{i=1}y_i$
And through a lot of math, we could also express $\hat{\beta_1}$ as $\hat{\beta}_1=\frac{s_y}{s_x}\hat{p}_{x,y}$. In other words, the slope of a model is the ratio of standard deviations, scaled by the correlation between predictor and response variables. 

### Homoscedasticity
This means that the variance of the errors $\epsilon_i$ does not depend on the predictor $X_i$. The opposite of this, where the variance of the error terms varies with $X_i$, is called heteroscedasticity, and is an issue to linear regression. 

### Q-Q Plot
Q-Q plot displays the quantiles of observed data against the quantiles of the normal distribution. It should look like a straight line with slope 1. This is a good way of checking heteroscedasticity. 

Another note on trusting linear regressions, extreme values should be taken with caution. For information on how to assess a model fit, check [[Multiple Regression]].
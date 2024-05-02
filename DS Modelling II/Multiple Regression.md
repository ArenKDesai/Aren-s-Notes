#Stat340 #Statistics #Regression #LinearRegression #MultipleRegression #ML #UWMadison

Extension of [[Prediction]]

### Multiple Predictors
Some response variables may be predicted with more than one predictor variable. They can be fit into a modified equation with $p$ predictors $y=\beta_0+\beta_1X_1+\beta_2x_2+...+\beta_px_p$. 
This creates $Y_i=\beta_0+\beta_1X_{i,1}+\beta_2X_{i,2}+...++\beta_pX_{i,p}+\epsilon_i$. 
An important thing to note is that these coefficients no longer correspond to a direct increase in the response variable. Now, an increase of 1 unit in a predictor variable corresponds to a $\beta_i$ increase in the response variable *while holding the other predictors fixed*. This is also said to be controlling for the other predictors. 

### Assessing Model Fit
$RSS=SSE=\sum^n_{i=1}(y_i-\hat{y_i})^2=\sum^n_{i=1}(y_i-(\hat{\beta_0}+\hat{\beta_1x_i}))^2$
Adding more predictor variables will trivially decrease RSS, so RSS needs to be renormalized. This is usually done by dividing it by degrees of freedom $n-(p+1)$, and then the square root is taken to transform it into the **residual standard error** (RSE). 

### $R^2$ 
Also explored in [[Variable Selection]]. The $R^2$ can be defined with $R^2=1-\frac{RSS}{TSS}$. $TSS=\sum^n_{i=1}(y_i-\hat{y})^2$. When $R^2$ is close to 1, the linear model is most likely accurate. 

### Mean Sum of Squares
Another way of model validation. This is the sum of squares between the model and the basic model $Y_i=\beta_0$. The equation for it is $\sum^n_{i=1}(\hat{y_i}-\bar{y})^2$. This should be **large** if the model is a good fit. This can be adjusted with RSS with $\frac{MSS/p}{RSS/(n-p-1)}$, which follows the F distribution. This can tell us if our model has no explanatory power. On a summary of a linear regression, this can be seen at the bottom with a p-value associated with the null hypothesis that the linear regression has no explanatory power. 

### Categorical Variables
Variables that are exhibited with a 0 or 1 are binary variables, which are often called dummy or indicator variables. If you have multiple categories, for right now, we'll split that into a predictor variable for each category, like a one-hot vector. 

Some variables can have interaction, where the effect of one predictor depends on another predictor. This can be handled by adding a predictor variable that is the product of those two variables. This is done in R like this:
```r
lm.model = lm(resp ~ 1 + pred1 + pred2 + pred1:pred2, data=data)
```
Also, if there appears to be a non-linear trend to the data, you can modify a variable like this:
```r
lm.model = lm(resp ~ 1 + pred + I(pred^2), data=data)
```
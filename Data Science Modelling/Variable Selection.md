#R #Stat340 #ML #Statistics #CrossValidation  #UWMadison

p is the number of predictors in a regression, k is the number of coefficients, so k = p+1
If p is too large, estimates of the coefficients can be very unstable
Take the model that has the minimum residual sum of squares (RSS). Doesn't work, as having another predictor will only decrease RSS.

Note: some important notes on variable manipulation can be found in [[Multiple Regression]].

### Overfitting and Unseen Data
Overfitting when it comes to regression occurs when there are too many predictors fit to the model, so the model simply memorizes the dataset. This can be counteracted by analyzing mean squared error (MSE):
$\mathbb{E}(\hat{Y}_{n+1}-Y_{n+1})^2$.
We split our data into a training set and a validation set in order to accomplish this. 

### Single-Split
Split the dataset in half, train on one half, validate on the other. Pro: Only have to fit the model once. Con: Only use half the data. This is a biased estimate. 

### Leave-One-Out
1. Take out one observation
2. Train the model on the rest of the observations
3. Evaluate the model on that single observation
When this is done for every observation in the set, it is leave-one-out cross-validation. This is an unbiased estimate. This also has the most variance out of the three. 
Pro: Model fit is good
Con: Takes a lot of time and resources. 

## K-fold Cross Validation
Randomly divide the data into K folds. For each fold, train the model on the rest of the data, then validate on the fold. This is a good medium with comparatively less variance. 
Better version of this covered in [[Stratified K-Fold Cross Validation]]. 

## Best Subset Selection
Fit literally every possible combination of variables, and keep the best. This is highly computationally expensive, but will result in the overall best model (measured by RSS). 

## Forward Stepwise Selection
Start with null model (*M0*), and for each predictor in *p* (predictor set), add the one that yields the biggest improvement in RSS. Use CV or something else to choose among *Mo* - *Mp*. 
Ends up fitting $1+\frac{p(p+1)}{2}$ models. 

## Backward stepwise selection
Start with the full model, and remove predictors one at a time. Always remove predictor that increases RSS the least. 

Hybrid approaches work, but aren't really better than the previous two. 

## Model Comparison Statistics

### Adjusted RSS
$1-\frac{RSS/(n-k)}{TSS(n-1)}$
Always slightly less than R^2. Is a good statistical measure of how good a model is. 

### Akaike Information Criterion (AIC)
-2ln(*L*)+2*k*

### Bayesian information criterion
-2ln(*L*)+*k*ln(*n*)

### Shrinkage
Fit a model with all available predictors, then modify loss function to set all unhelpful predictors to 0. Also known as regularization. This is continued in [[Ridge Regression & LASSO]]. 
#CrossValidation #Statistics 

Referencing the [GeeksForGeeks article](https://www.geeksforgeeks.org/stratified-k-fold-cross-validation/#). 

## K-Fold Cross Validation
Also covered in [[Variable Selection]], **k-fold cross validation** is used to compare difference randomly-fit models on $K$ folds of the data set. Imagine a stack of data, and slicing that data with $K$ even slices. We train a model on each slice, and compare to find the best model. 
However, this fails if the classes we're modelling for are unbalanced. For example, imagine we have a dataset of penguin traits, and we're predicting what species of penguin we're looking at. If 80% of the dataset is Emperor penguins, the 4 of the 5 model 
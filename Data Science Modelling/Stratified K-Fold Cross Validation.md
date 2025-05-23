#CrossValidation #Statistics 

Referencing the [GeeksForGeeks article](https://www.geeksforgeeks.org/stratified-k-fold-cross-validation/#). 

## K-Fold Cross Validation
Also covered in [[Variable Selection]], **k-fold cross validation** is used to compare difference randomly-fit models on $K$ folds of the data set. Imagine a stack of data, and slicing that data with $K$ even slices. We train a model on each slice, and compare to find the best model. 
However, this fails if the classes we're modelling for are unbalanced. For example, imagine we have a dataset of penguin traits, and we're predicting what species of penguin we're looking at. If 80% of the dataset is Emperor penguins, the 4 of the 5 models may only see Emperor penguins, so they'll pick Emperor penguins for 100% of the instances. 

Thus, we use **stratified k-fold cross validation**, which splits the dataset into $K$ folds that hold the correct ratio of categories. In Python, this looks like:
```Python
from sklearn.model_selection import StratifiedKFold

x = ... 
y = ...
model = ...

skf = StratifiedKFold(n_splits=int, shuffle=True, random_state=int)
scores = []

for train_index, test_index in skf.split(x, y):
	x_train_fold, x_test_fold = x[train_index], x[test_index]
	y_train_fold, y_test_fold = y[train_index], y[test_index]
	model.fit(x_train_fold, y_train_fold)
	scores.append(model.score(x_test_fold, y_test_fold))
```
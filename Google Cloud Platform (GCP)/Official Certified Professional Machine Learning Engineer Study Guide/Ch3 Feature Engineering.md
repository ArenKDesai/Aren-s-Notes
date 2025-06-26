Data transformations are typically done before training or testing the model, but this can lead to skew during deployment. Thus, some models can transform the data during testing. 

One feature engineering technique that can transform numeric data into categorical data is bucketing. For example, using latitude and longitude can be computationally expensive, but using ranges of lat and lon can be a categorical fix. This can be done with ranges or quartiles. 

A special feature category called Out of Vocab can be created to trash outliers. 

AUC ROC is used for a balanced dataset in classification problems that have an equal number of examples for both classes
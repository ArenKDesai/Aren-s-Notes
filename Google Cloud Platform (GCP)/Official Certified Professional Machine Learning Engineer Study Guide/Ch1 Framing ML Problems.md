You can break ML problems into supervised and unsupervised problems. Unsupervised problems are solved via clustering algorithms or autoencoders, which reduce the dimensionality of input data ([[Principal Component Analysis]]).  Another use case is *topic modelling*, which clusters sets of documents. 
Supervised problems sometimes use classification algorithms. The Cloud Vision API can classify millions of different objects in a picture for example. Other supervised techniques are regression and forecasting. 

There are multiple metrics used to fit ML models. One for binary classification is recall:
$\text{Recall}=\frac{\text{True Positive}}{\text{True Positive + False Negative}}$
Recall is good for having a low false negative rate. Another, good for reducing false positives, is precision:
$\text{Precision}=\frac{\text{True Positive}}{\text{True Positive + False Positive}}$
And a metric that combines both is the F1 score:
$\text{F1}=2\times\frac{\text{Precision * Recall}}{\text{Precision + Recall}}$

The Area Under the Curve Receiver Operating Characteristic (AUC ROC) plots the performance of a binary classification model. The false positive versus true positive rate is plotted. The top left corner is the (unobtainable) ideal. This method is scale-invariant and is classification-threshold invariant (helps measure the model regardless of threshold). 
![[aucroc_curve.png]]
However, AUC ROC being classification threshold-invariant can be a downside if you want to factor in the classification threshold, in which case the Area Under the Precision-Recall (AUC PR) Curve is plotted. This is beneficial to heavily skewed datasets. 

There's a number of target metrics. Here's a few:
- MAE: generic, but good.
- RMSE: penalizes the model for incorrectly predicting very large values. 
- RMSLE: penalizes under-prediction. 
- MAPE: cares about proportional difference between actual and predicted. 
- R^2: generally shows a better fitting model. 

You can break ML problems into supervised and unsupervised problems. Unsupervised problems are solved via clustering algorithms or autoencoders, which reduce the dimensionality of input data ([[Principal Component Analysis]]).  Another use case is *topic modelling*, which clusters sets of documents. 
Supervised problems sometimes use classification algorithms. The Cloud Vision API can classify millions of different objects in a picture for example. Other supervised techniques are regression and forecasting. 

There are multiple metrics used to fit ML models. One for binary classification is recall:
$\text{Recall}=\frac{\text{True Positive}}{\text{True Positive + False Negative}}$
Recall is good for having a low false negative rate. Another is precision:
$\text{Precision}=\frac{\text{True Positive}}{\text{True Positive + False Positive}}$
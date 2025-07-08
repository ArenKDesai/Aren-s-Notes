There are two types of explainability:
1. Global: overall ML model is transparent and comprehensive
2. Local: explaining the model's individual predictions

Shapely allows you to try to attribute the importance of features in a black-box model. 
Integrated gradients efficiently computes feature attributions for local feature importance, but not global. 
XRAI assess overlapping regions of the 
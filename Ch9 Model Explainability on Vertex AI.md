There are two types of explainability:
1. Global: overall ML model is transparent and comprehensive
2. Local: explaining the model's individual predictions

Shapely allows you to try to attribute the importance of features in a black-box model. Shapely is only for tabular data. Shapely is important for non-differentiable models, such as models with rounding capabilities. 
Integrated gradients efficiently computes feature attributions for local feature importance, but not global. Integrated gradients work on either tabular or image data. 
XRAI assess overlapping regions of the image to create a saliency map, highlighting relevant regions of an image rather than pixels. XRAI only works on image data. 
There are traditionally three methods of solving ML problems:
1. Pretrained
2. AutoML
3. Custom
Typically, solving an ML problem starts with a pretrained model since it's the fastest and easiest method. You move down to AutoML or custom models accordingly. 

Google pretrained models are:
1. Vision AI
2. Video AI
3. Natural Language AI
4. Translation AI
5. Speech-to-Text and Text-to-Speech AI
and solutions that include pretrained models include:
6. Document AI
7. Contact Center AI

Structured data with well-defined schemas typically take advantage of BigQuery ML or Vertex AI Tables. 
Classification problems with a table typically use the metrics AUC ROC, AUC PR, Logloss, Precision at Recall, and Recall at Precision. 
Regression problems with a table typically use RMSE, RMSLE, MAE. 
Forecasting problems with time-series data typically use RMSE, RMSLE, MAPE, and Quantile loss. 

AutoML jobs in the console can be set with the maximum number of hours that the job can run for, or the minimum. 

For forecasting specifically, developers can use AutoML, Seq2seq+ (good for datasets of less than 1GB), or temporal fusion transformers. 

AI for images and video includes:
1. Image classification (single)
2. multiclass classification
3. object detection
4. image segmentation
5. video classification
6. action recognition
7. object tracking

AutoML also includes AutoML Edge, which can be deployed to edge devices (pixel, samsung, etc) and edge TPUs. 

AutoML for text includes text classification, multilabel classification, entity extraction, and translation. 

GCP also has an AutoML solution specifically for the retail domain: Retail Search. It essentially allows retailers to use search algorithm similar in quality to Google's. 
A similar product exists called the Vision API Product Search, which allows products to be searched via an image. 
There's also Recommendations AI, which allows nuances behind customer behavior, context, and SKUs 
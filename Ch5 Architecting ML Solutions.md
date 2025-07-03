ML pipelines have the following steps:
1. Data collection
2. Data transform
3. Model training
4. Model tuning
5. Model deployment
6. Model monitoring

Google Vertex AI training works well for custom model training since the spinning up of infrastructure for training or managing said infrastructure. Vertex AI AutoML and APIs work well for pretrained or auto models as well. Vertex AI hyperparameter tuning can automate running multiple training jobs in a scalable manner, and Vertex AI Experiments can track variables and multiple training results in a managed, scalable, and reliable manner. 

Try to avoid storing data in network file systems or virtual machines, and also avoid storing data in Cloud SQL. BigQuery, Google Cloud Storage, and NoSQL data store are all better options. 


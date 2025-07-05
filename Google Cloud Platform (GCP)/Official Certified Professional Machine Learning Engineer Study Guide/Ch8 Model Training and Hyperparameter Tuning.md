Steps to training ML models with structured/semi-structured/unstructured data:
1. Collect. GCP services include:
	1. Pub/Sub and Pub/Sub Lite, which are scalable for messaging and real-time analytics. They both work well with Dataflow and other processing services, and BigQuery and analytics services. Lite is good for predictable and consistant loads. 
	2. Datastream, good for moving existing databases to GCP. 
	3. BigQuery Data Transfer Service, which transfers data from warehouses like Teradata and Amazon Redshift, external cloud providers such as Amazon S3, and Google SaaS apps like Cloud Storage, Google Ads, etc. 
2. Process
	1. Cloud Dataflow is a serverless, fully managed ETL service
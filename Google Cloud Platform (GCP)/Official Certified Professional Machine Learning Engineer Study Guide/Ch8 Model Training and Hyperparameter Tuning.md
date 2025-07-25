Steps to training ML models with structured/semi-structured/unstructured data:
1. Collect. GCP services include:
	1. Pub/Sub and Pub/Sub Lite, which are scalable for messaging and real-time analytics. They both work well with Dataflow and other processing services, and BigQuery and analytics services. Lite is good for predictable and consistant loads. 
	2. Datastream, good for moving existing databases to GCP. 
	3. BigQuery Data Transfer Service, which transfers data from warehouses like Teradata and Amazon Redshift, external cloud providers such as Amazon S3, and Google SaaS apps like Cloud Storage, Google Ads, etc. 
2. Process
	1. Cloud Dataflow is a serverless, fully managed ETL service that offers exactly-once streaming semantics that reduces MapReduce performance problems. 
	2. Cloud Data Fusion is covered in [[Ch3 Feature Engineering]].
	3. Cloud Dataproc: fully managed and highly scalable service for apache spark/flink/presto and more. It has integration with other services like Storage/BigQuery/Bigtable/Logging/Monitoring. Connectors that connect to Dataproc include:
		1. Cloud Storage Connector, which is available by default. Helps run Hadoop or Spark jobs directly on data in Cloud Storage
		2. BigQuery Connector: Enables Spark/Hadoop applications to process data from BigQuery and write to BigQuery. 
		3. BigQuery Spark Connector: Supports reading Google BigQuery tables into Spark DataFrames, then writing DataFrames back to BigQuery. 
		4. Cloud Bigtable with Dataproc: Excellent for Spark or Hadoop uses that require Apache HBase
		5. Pub/Sub Lite Spark Connector: self-explanatory
	4. Cloud Composer
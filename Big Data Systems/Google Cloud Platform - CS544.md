#CS544 #Cloud #GoogleCloud #UWMadison #BigQuery

## Compute
### VMs
Virtual machines that you can specify GPU type, number of GPUs, machine type, etc. 
Multi-tenant hosts are VMs with multiple customers, sole-tenant are VMs what all share one customer. 
#### Billing Models
VM deployment has on-demand instances of a constant high price and spot instances.
The billing models include fixed, auto scaling (cloud detects high/low load and scales), or pay-as-you-go with fine-granularity, like AWS Lambda. 

## Memory
IaaS - Memory oriented and optimized, more expensive but more freedom. 
PaaS - full service. Less freedom, cheaper. Caches rows. 

## Storage
HDDs and SDDs, price depends on size and type

## Network
Continents > regions > zones
A region is a data center consisting of 1 or more buildings. Zones are regions, so certain subsets of one data center are certain zones. 
Ingress (data coming in) is usually free, egress (data going out) you pay for. It also depends on internet, continent, region, zone, etc. 

## BigQuery
- When doing a query, the ```FROM``` clause has to have an ```AS``` statement since you can't typically reference the dataset itself. For example, 
```SQL
FROM 'bigquery-public-data.geo_us.boundaries.counties' AS counties
```
BigQuery uses Colossus Storage, so that is what's billed. 
BigQuery is based on Dremel and can run queries on other data sources. 
It uses data warehouses (BQ query engine with BQ storage) and lakes. 
Typically, optimization is on run-length encoding and dictionary encoding. 

### Parameterization
Queries can be parameterized in order to reduce redundant calls. These are denoted by the @ symbol. 

### Machine Learning
Bigquery has a DATA_SPLIT_METHOD config which does the following:
- < 500 rows: 100% training data
- < 50K rows: 80% training data
- > 50K rows: 10K rows for test, rest for training
This splitting can be disabled with DATA_SPLIT_METHOD="NO_SPLIT", or by manually splitting with ```rand()<ratio```. 

You can train like so:
```
CREATE OR REPLACE MODEL myproj.mydataset.mymodel
OPTIONS(MODEL_TYPE='LINEAR_REG', INPUT_LABEL_COLS=['temp'])
AS
SELECT yesterday_temp, humidity, temp
FROM weather
```

## Colossus
Users can create buckets that contain objects (or files). Applications can switch HDFS and GCS. 
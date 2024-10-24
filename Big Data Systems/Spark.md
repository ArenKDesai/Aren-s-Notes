#CS544 #UWMadison #FileSystems #Spark #SparkSQL

Spark combines the [[Map Reduce]] pipeline into one large operation. 

### Resilient Distributed Datasets
- data lineage: record series of operations on other data necessary to obtain results
- lazy evaluation: computation only done when results needed
- immutabilty

Data lineage comes in the form of two types of functions:
1. Transformation (parallelize, map, filter, etc)
2. Action (collect, etc)

When you write an RDD that does a transformation, no actual work is done immediately. An action has to be called first, such as collect. ex:

![[Screenshot from 2024-10-21 11-05-50.png]]

Spark code is converted to jobs, which consist of stages, which consist of tasks. Tasks run on a single CPU core and operate on a single partition. 

If there are too many partitions running, repartitioning can be used to run everything faster. This comes at a cost, as repartitioning is slow. This sends data over the network. 

Another event sending data over the network is transformations. 

### Transformations
- Narrow: filtering
- Wide: sorting, often use network resources, unless all input partitions are on the same machine. 

### [[Caches]]
Some RDDs might get used repeatedly, so they're cached. We can also do this manually with sc.cache(), and uncaching with sc.unpersist(). 

# Spark Deployment

## Standalone
- Can run on any node in cluster
- each node in cluster will launch its own YARN
- Can be allocated arbitrarily to any host in the cluster YARN's resource

## Local
- Runs on a single JVM, like a laptop or single node
- Often used for testing / development
- Run on the same JVM as driver
- Runs on the same host

# Spark SQL
- builds on RDDs
- Just for people who know SQL but not Python, Java, etc. 
ex
```
from pyspark.sql.functions import col, expr

col("x")
col("x") + 1
exor*x+1").alias("plusone")
df2=df.withColumn("station", expr("substring(value,0,11)"))
```
## DataFrame API
- For people who like dataframes in, for example, pandas. 
- Dataframes are mutable, while RDDs are immutable
ex
```
!hdfs dgs -du -h hdfs://nn:9000/sh.csv
df = (
	spark.read_format("csv")
	.option("header", True)
	.option("inferSchema", True)
	.load("hdfs://nn:9000/sf.csv")
)
```


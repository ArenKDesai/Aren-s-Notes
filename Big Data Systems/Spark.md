#CS544 #UWMadison #FileSystems #Spark #SparkSQL #ML #SparkML

Spark combines the [[Map Reduce]] pipeline (map and reduce) into one large operation. 

### Resilient Distributed Datasets
- data lineage: record series of operations on other data necessary to obtain results
- lazy evaluation: computation only done when results needed
- immutabilty

Data lineage comes in the form of two types of functions:
1. Transformation: create a new RDD (parallelize, map, filter, etc)
2. Action: perform all operations in the graph to get an actual result (collect, etc)

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

### Schema inferencing
Explicit scheming is much faster, but more difficult to code. For example,

```
df = (spark.read.format("csv")
	.option("header", True)
	.option("inferSchema", True)
	.load("hdfs://nn:9000/sf.csv))
```
is schema inferencing which includes 17 tasks and 33 seconds, and has to read the whole file. 

```
df = (spark.read.format("csv")
	.option("header", True)
	.load("header", True))

df = (spark.read.format("csv")
	.schema("???")
	.load("hdfs://nn:9000/sf.parquet"))
	
df = (spark.read.format("parquet")
	.load("hdfs://nn:9000/sf.parquet"))
```
is schema non-inferencing, which is 2 tasks and < 1 second, along with reading less than the whole file. 

## Physical Execution
When shuffling partitions, we call ```spark.sql.shuffle.partitions```, which defaults to 200 partitions. There are three optimizations that can be done:
1. partial aggregates, or computing partial results before the exchange (saves network I/O)
2. ```spark.sql.adaptive.coalescePartitions.enabled```, which combines smaller partitions into larger ones
3. ```bucketBy```, which means formatting the data during the set creation. 

## Demo
```{Python}
spark.sql("""
SELECT Call_Type, COUNT(*)
FROM calls
GROUP BY Call_Type
""").explain('formatted')

(spark.table("calls")
.sample(True, 0.1)
.write
.mode("overwrite")
.bucketBy(10, "Call_Type")
.saveAsTable("calls_by_type"))
```

## Joins

### Shuffle Sort Merge Join
Tables are transferred over the network, and data is grouped individually on partitions. Each table goes over the network once. 

### Broadcast Hash Join
Keep the table in memory and compute the join in a loop. 

# Spark Machine Learning
```{Python}
# sci-kit learn
model = ???
model.fit(X,y)
y = model.predict(X)

# pytorch
model = ???
for epoch in range(???):
	for X,y in ???:
		...
y = model(X)

# spark mlib
import pyspark.ml
unfit_model = ??? # spark mlib models are immutable
fit_model = unfit_model.fit(df)
df2 = fit_model.transform(df)
```

### Terminology

- Transformer
	- object has .transform method
	- takes a DataFrame, returns original + 1 or more column
- Estimator
	- object has a .fit method that returns a new object
	- an unfitted model is an estimator; calling .fit returns a fitted model (transformer)

```
import pandas as pd
import numpy as np

df = pd.DataFrame("x1":..., "x2":...)
df["y"]=df["x1"] + df["x2"]
df = spark.createDataFrame(df)

train, test = df.randomSplit([0.75, 0.25], seed=42)
train.write.format("parquet").mode("ignore").save("hdfs://nn:9000/train.parquet")
test.write.format("parquet").mode("ignore").save("hdfs://nn:9000/test.parquet")

train = spark.read.format("parquet").load("hdfs://nn:9000/train.parquet")
test = spark.read.format("parquet").load("hdfs://nn:9000/train.parquet")

# ML part
from pyspark.ml.regression import DecisionTreeRegressor # Unfit
from pyspark.ml.regression import DecisionTreeRegressionModel # Fit

dt = DecisionTreeRegressor(featuresCol="x1", labelsCol="y")
dt.fit(train)
```
The above will break, and will need this:
```
from pyspark.ml.feature import VectorAssembler
va = VectorAssembler(inputCols=("x1", "x2"), outputCol="features")
va.transform(train).show()
model = dt.fit(va.transform(train))
model.transform(va.transform(test))

from pyspark.ml.pipeline import Pipeline # unfit
from pyspark.ml.pipeline import PipelineModel # fit

pipe = Pipeline(stages=([va,dt]))
model = pipe.fit(train)
# model.stages().toDebugString will print the actual tree

# save model and load on another machine
model.write().overwrite().save("hdfs://nn:9000/model")
model2 = PipelineModel.load("hdfs://nn:9000/model")
```
Now, let's test how good the model is.
```
from pyspark.ml.evaluation import RegressionEvaluator
r2score = RegressionEvaluator(metricName="r2score", labelCol="y", predictionCol="prediction")
r2score.evaluate(model.transform(test))
```

## Decision Trees
Similar to [[Classification Trees]]. To choose splits:
1. Sort data by each column
2. calculate impurity for each split (one pass)

If rows are too large to fit in RAM on one worker, you use the PLANET algorithm. 

### PLANET Algorithm
Parallel Learner for Assembling Numerous Ensemble Trees. Originally for MapReduce. Spark's pyspark.ml use this. 
Steps:
1. Create a histogram where each bin has approx. the same number of samples. 
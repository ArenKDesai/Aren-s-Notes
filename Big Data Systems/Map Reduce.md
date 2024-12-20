#UWMadison #CS544 #MapReduce #FileSystems 

Runs on top of file systems like HDFS (see [[Hadoop File System]]). 

A database structure can be too limiting if you have multiple forms of data that require multiple formats to be read faster and more efficiently. 

MapReduce has its own query language, which is much more difficult to write than sql. 
Ex:

```{SQL}
SELECT color FROM table WHERE shape="square"
```
This is equal to this MapReduce pseudocode (typically written in java):
```
def map(key, value):
	if value.shape = square:
		emit(key, value.color)
```

These "Mappers" will run on multiple machines at once. The input data is sent to a cluster of machines with the mappers. 

In between the Map phase and the Reduce phase, there's a Shuffle phase, which brings together related keys, and all the related keys are brought in to one Reduce call. 

Users can also write "Reducers", which can either output exactly their input or have further computation. 
Example:
```
def reduce(key, values):
	count = 0
	for row in values:
		count += 1
	emit(key, count)
```

Reducers combine the output of multiple mappers to a single file. MapReduce shuffles the data, brings together intermediate outputs from mappers with the same key. All data with the same key is passed to a single reduce call. 

Each reduce task produces one output file. A reduce task might take multiple keys. A single reduce call takes a single key and all corresponding values. All intermediate rows with the same key go to the same reducer. 
## Overview
Map Phase
- SELECT, WHERE, GROUP BY, JOIN
Shuffle Phase
- ORDER BY, GROUP BY, JOIN
Reduce Phase
- SELECT, AGGREGATE, HAVING, JOIN

## Data Locality
Goal: Avoid network transfers

HDFS DataNodes and MapReduce executor run on the same machines, on the same cluster. This uses the disk and not the network, which would be a large bottleneck. 

## Pipelines: Sequence of Map reduce Jobs
HDFS files get sent to Mapping jobs into reduce jobs into HDFS files, and the cycle continues. Intermediate transfers can screw over optimization algorithms, so [[Spark]] is needed to fix this. 


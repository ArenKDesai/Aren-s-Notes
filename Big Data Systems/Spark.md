#CS544 #UWMadison #FileSystems #Spark

Spark combines the [[Map Reduce]] pipeline into one large operation. 

### Resilient Distributed Datasets
- data lineage: record series of operations on other data necessary to obtain results
- lazy evaluation: computation only done when results needed
- immutabilty

Data lineage comes in the form of two types of functions:
1. Transformation (parallelize, map, filter, etc)
2. Action (collect, etc)

When you write an RDD that does a transformation, no actual work is done immediately. An action has to be called first, such as collect. ex:
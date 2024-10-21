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

![[Screenshot from 2024-10-21 11-05-50.png]]

Spark code is converted to jobs, which consist of stages, which consist of tasks. Tasks run on a single CPU core and operate on a single partition. 

If there are too many partitions running, repartitioning can be used to run everything faster. This comes at a cost, as repartitioning is slow. This sends data over the network. 

Another event sending data over the network is transformations. 

### Transformations
- Narrow: filtering
- Wide: sorting, often use network resources, unless all input partitions are on the same machine. 

### [[Caches]]
Some RDDs might get used repeatedly, so they're cached. We can also do this manually with sc.cache(), and uncaching with sc.unpersist(). 


## Spark SQL
- builds on RDDs
- Just for people who know SQL but not Python, Java, etc. 

## DataFrame API
- For people who like dataframes in, for example, pandas. 
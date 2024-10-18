#UWMadison #CS544 #MapReduce #FileSystems 

Runs on top of file systems like HDFS (see [[Big Data File Systems]]). 

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
#CS544 #UWMadison #FileSystems #GoogleFileSystem #GFS

Problem: making a database with a small dataset in mind, then your userbase grows massively

Idea: partition your database into multiple servers (scaling out)
Problem: Splitting data inevitably leads to problems. 
Another problem: one server dies, no fault tolerance is esablished

## Google File System
Idea: Base everything on lots of cheap, commodity hardware
Contains MapReduce, BigTable -> GFS -> multiple worker machines w/ hard drive disks (or other storage). 
GFS is the file system
BigTable is the database
[[Map Reduce]] is for analytics

## Hadoop File System
Multiple DataNode Computers (one DataNode computer can be multiple hard drives) partitioned into blocks. Files are split into these blocks. 

Files get replicated with a replication number in case a server dies. 
When a file gets replicated, each data node will take the burden to send it to the next datanode. 

The name nodes contain information about the datanodes (like a map for queries to datanodes). 

Use PyArrow to read Hadoop files.
```
import pyarrow as pa
import pyarrow.fs # file systems
import io

hdfs = pa.fs.HadoopFileSystem("main",9000)
with hdfs.open_input_file("/data/v2.txt") as f:
	reader = io.TextIOWrapper(io.BufferedReader(f))
	for line in reader:
		print(line, end="")
```
## Hadoop Operations

You can run shell commna
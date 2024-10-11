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
MapReduce is for analytics

## Hadoop File System
Multiple DataNode Computers partitioned into blocks. Files are split into these blocks. 
ex: 
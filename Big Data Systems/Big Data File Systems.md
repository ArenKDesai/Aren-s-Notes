#CS544 #UWMadison #FileSystems

Problem: making a database with a small dataset in mind, then your userbase grows massively

Idea: partition your database into multiple servers (scaling out)
Problem: Splitting data inevitably leads to problems. 
Another problem: one server dies, no fault tolerance is esablished

## Google File System
Idea: Base everything on lots of cheap, commodity hardware
Contains MapReduce, BigTable -> GFS
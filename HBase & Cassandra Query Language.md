
Column-oriented and non-relational in sparse tables. Data is indexed with a unique row key. Data is kept in memory until large, then written to disk in one large write. 

No boss node, many workers. Clusters are *rings* due to adjacency. Ring organization doesn't have to adhere to network topology. 
Inserts are *upserts* since they also update. 
Keyspaces are databases which store data across many workers. Different keyspaces can have their own replication settings, and each keyspace may contain many tables. 

Rows are emphasized, even if it means one row has millions of columns. 
### Custom types
```
cass.execute("""
create type FullName (
	first Text,
	last Text
)
""")

cass.execute("""
alter table loans add (username FullName);
""")
```

## HDFS & Spark vs Cassandra
HDFS will struggle with a lot of small files. Spark is fine since it's built to work with small rows. 

*Incremental Scalability*: can we efficiently add more machines into a cluster?
HDFS is better at this.  

For locations, HDFS uses mapping from the namenode and Spark uses hasing partitions. Dynamo and Cassandrax




Column-oriented and non-relational in sparse tables. Data is indexed with a unique row key. Data is kept in memory until large, then written to disk in one large write. HBase is layered on HDFS. 

No boss node, many workers. Clusters are *rings* due to adjacency. Ring organization doesn't have to adhere to network topology. 
Inserts are *upserts* since they also update. 
Keyspaces are databases which store data across many workers. Different keyspaces can have their own replication settings, and each keyspace may contain many tables. 

Rows are emphasized, even if it means one row has millions of columns. They're never split across regions, as HBase only supports single-row transactions. 
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

In a cluster, you find tokens, which lead to nodes. Tokens are added one at a time so there are no collisions. 

V-Nodes also solve the collision issue. 


# Replication
We replicate to improve durability - same as [[Map Reduce]]. 

map: 1={1,2}, 2={3,4}, 3={5,6}, 4={7,8}
workers: 1,2,1,4,3,4,2,3

```
create keyspace X
with replication={'class': 'SimpleStrategy',
	'replication_factor': 2};}

create keyspace Y
with replication={'class': 'SimpleStrategy',
	'replication_factor': 3};}
```

### Policy
Replication polices are pluggable, with built-in strategies

SimpleStrategy: all nodes equal, skip vnodes on same machine, ignore placement
NetworkTopologyStrategy: consider data centers/racks. When walking the ring, some vnodes may be skipped to protect against correlated failure. 

### Quorum
Sets how many nodes will respond when we define the write and read polices in Cassandra. 
If you want reads to see the latest successful write, you should have $RF < W+R$. 

## Worksheet
Token Map:
token(n1)=(-2,4), token(n2)=(-6,0), token(n3)=(-4,2,5)
Problem 1: how many nodes / vnodes are there?
Ans: 3, 7
Problem 2: which node likely has the best resources?
Ans: 3
Problem 3: one of the vnode positions of n2 is drawn in the ring below. Draw the rest:

$\begin{matrix}0&&0&&n2&&0&&n3&&0&&n1&&0&&n2&&0&&n3&&0&&n1&&n3&&0&&0\\-8&&-7&&-6&&-5&&-4&&-3&&-2&&-1&&0&&1&&2&&3&&4&&5&&6&&7\end{matrix}$
Problem 4: what ring positions are in the wrapping range?
Ans: 6+7
Problem 5: what node is responsible for each token? 4,1,6
Ans: n1,n3,n2
Problem 6: primary key is (A,B), which is one partition column followed by one cluster column. Which node owns this row? Token(A)=-3, Token(B)=-6, Token((A,B))=3
Ans: -3

Problem 8: assuming 2x replication, what are the positions of the vnodes for a row with token -1?
ans: n2+n3, and 0+2
Problem: 3x, positions of vnodes responsible for a row with token 1?
ans: 2+4+-6
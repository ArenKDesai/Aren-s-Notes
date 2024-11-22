#UWMadison #CS544 

Most forms of program communication are synchronous, where both parties have to be ready and participating. However, in **streaming**, the communication is asynchronous. A client send information that a broker handles, and the recipient handles it whenever the recipient is ready. 

Kafka is a system to manage a complex system of I/O subsystems, considered a logging system. It is also closely integrated with [[Spark]] in Python. 

### Topics
Kafka topics are managed by brokers (servers) that receive messages from producers and categorize them to be managed / sent to consumers that subscribe to the topics. Very similar to [[ROS and ROS2]]. 

Consumer message receiving typically run a ```poll()``` loop permanently. This loop processes the new data. 

### Messages
Parts:
- key (optional): some bytes
- value (required): some bytes

The value is typically a data structure with many values, like a dict. Protocol buffers from [[gRPC]] could be used to process these messages as well. 

When messages are written, it might contain only a value, in which case the producer rotates between partitions. This is called a **round-robin policy**. If the message has a key, the key can be hashed, and the same keys will go to the same partition. 

Messages are partially ordered, which means they can sometimes be compared like integers, sometimes not. If $A$ and $B$ share the same topic and key, then $B$ was produced after $A$, and we say $B$ happened after $A$. Each consumer group of the topic will consume $A$ before $B$. No keys = no guarantee what order messages are consumed. 
### Poll
The consumer's poll function returns batches when there's either enough data or there's a timeout. The batches contain some subset of partitions, and there's some number of messages in a partition, starting at the offset. Offsets are saved as the value from a dict of origins (like clicks). 

The consumer would have to "seek" offsets. Consumers are grouped and each group gets their own offsets. 

ex:
```Python
batch = consumer.poll(1000)
for topic, messages in batch.items():
	print("partition", topic.partition)
	for msg in messages:
		print(msg.value)
```
### Partitions
In each partition (group), we need to know which consumers are in charge of which offsets. This can be a manual assignment with code, or Kafka could be asked to do this automatically. In this case, Kafka assigns consumers partitions when they start polling. 

When a consumer exits or a consumer is grabbing batches, the offset alignments change. 

When a segment gets old, it can be deleted. This is done from the "left" (in queue terms), and never from the "right" or middle. Rollover and retention policies are configurable, but they can be set to size, time, etc. 

## Demo Notes
You have to format clusters before you start them. 

```Python
from kafka import KafkaAdminClient, KafkaProducer, KafkaConsumer

# Brokers
broker = 'localhost:9092'
admin = KafkaAdminClient(bootstrap_servers=[broker])
# admin.list_topics()
from kafka.admin import NewTopic
admin.create_topics([NewTopic("even_nums", replication_factor=1, num_partitions=1)])
admin.create_topics([NewTopic("odd_nums", replication_factor=1, num_partitions=2)])
# Producers
producer = KafkaProducer(bootstrap_servers=[broker])
result = producer.send("even_nums", bytes(str(0), 'utf-8'))
result.get()
# Set up a function to publish to topics repeatly. watch threading...
# Consumers
consumer = KafkaConsumer(bootstrap_server=[broker])
from kafka import TopicPartition
consumer.assign([TopicPartition("even_nums", 0)])
consumer.assignment()
batch = consumer.poll(1000)
for topic_partition, messages in batch.itmes() 
```

## Replication
RF 3 means that there will be 3 copies of a message. Each partition has one leader and RF-1 follower replicas. This means that one message will only be sent to one leader, the followers are constantly fetching messages from the leaders. How in-sync the followers are is tunable. 
There's also a setting called min.insync.replicas where if there are less than the minimum insync followers running, the leader refuses to store messages until the followers are back up. 
Larger min.sync = stronger durability, smaller min.sync = better availability. 
If the leader fails, the controller broker (chosen w/ help of Zookeeper or KRaft) elects an in-sync replica as new leader. 
If the number of concurrent broker failures < min.insync.replicas, then the committed data is safe. 
The leader also never lets consumers consumer un-commited messages, in the case that the consumer consumes it, then the leader goes down before sending it to the followers. This means that consumer fetches and follower fetches are two different types of fetch requests. 

Messages are idempotent if serializing the message multiple times just overwrites the data with the same message. Non-idempotent messages may cause duplicates in rare circumstances, which can be suppressed by keeping track of which messages have already been saved and not sending duplicates. 

Unlike [[HBase & Cassandra Query Language]], the order of message cannot change, s
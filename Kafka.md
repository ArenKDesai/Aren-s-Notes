#UWMadison #CS544 

Most forms of program communication are synchronous, where both parties have to be ready and participating. However, in **streaming**, the communication is asynchronous. A client send information that a broker handles, and the recipient handles it whenever the recipient is ready. 

Kafka is a system to manage a complex system of I/O subsystems, considered a logging system. 

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

When a segment gets old, it can be deleted. This is done from the "left" (in queue terms), and never from the "right" or middle. 
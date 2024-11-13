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
---
date: 2024-08-11
layout: zettel
category: showcase
link: https://www.youtube.com/watch?v=sa1SkPWifBk
tags:
  - data-streaming
title: architecture of kafka
article-name: Apache Kafka - Introduction & Architecture
---
- Architecture of 3 node [kafka](kafka.md) cluster ![](attachments/Pasted%20image%2020240817175609.png)

- Topics:
	- Similar to entity / table in data system
	- This include messages (aka records) created by kafka producers
	- Name of topic is unique across kafka cluster (just like table name is unique in database)
	- See also [kafka-topic-data-management](kafka-topic-data-management.md)
- Messages:
	- Kafka record in a topic
	- Consists of key-value pair and metadata
	- The messages do not have a specific data type. Usually its simple bytes or string
	- Message produced in a topic are identified by an offset number (an integer)
	- Metadata includes header, timestamp, topic name, partition number, etc.
	- Example	
	- ```
		{
			topic:"Customer",
			timestamp:"2024-06-05 T 20:17:46.384Z",
			partition: 0
			value {
				"id": 100,
				"name": "Ajit"
			}
		
		}```

- Partitions:
	- Typically kafka does not store all records of a topic in a single file and divides it across partitons.
	- In order to create topics, we'll need to specify following:
		- No. of partitions
		- Replication Factor
			- No of copies; also called partion replica or replica
			- should be less than or equal to numbers of brokers
		- Retention Period (default 7 days)
			- Data older than 7 days will be delated from kafka
		- 
	- There is also partition leader (among partitions) for a topic in one of the brokers. Producers only writes to the partition leader
	- In case if broker fails, one of the follower from other brokers will become a leader.
	- ![](attachments/Pasted%20image%2020240817183617.png)
	- Eg: A topic A created with 3 partitions and with replication factor:3 on 3 node kafka cluster.
		- ![](attachments/Pasted%20image%2020240817183807.png)
		- Replicas id are essentially broker ids
		- ISR = In sync replicas; which of these replicas are live.
		- 
- Kafka Brokers & Controllers:
	- Kafka Brokers
		- Essentially a kafka server application running on a host machine.
		- They store all the data created
		- Brokers can communicate with each other through interbroker communication.
	- Controller:
		- Its one of the brokers of Kafka Cluster and is responsible for administration of partition.
		- For example: It decides which replica should become new leader for each partition.
		- Tracks the state of each partition. (online, offline, delated, etc.)
		- ZooKeeper elects which broker should be a controller, if controller crashes/fails - Zookeeper elects new controller among brokers
		
- Zookeeper:
	- Its an application running outside of kafka cluster
	- Number of Zookeepers can be greater than 1; and they could work as a Zookeeper Cluster. The number of Zookeepers should always be odd number( Why ?)
	- Functions:
		- Tracks the state of kafka brokers (alive brokers, crashed brokers, etc)
		- Elects a new controller whenever a broker fails
		- contains metadata information.
			- list of topics and number of partition for each topic
			- location of all the replicas for each topic partition.
			- Information about ACLs - Access control lists; for example: for a producer, ACL contains all topics in which a producer is authorized to write data.
			- 
- Producers:
	- Data Producers: produce message to a topic; eg: backend application writing to a database system.
	- synchronous and asynchronous data producers; additional configuration options includes batch size, client identifiers, compression, and acknowledgements
	- How is data published? (aka: data publishing strategy)
		- if partitionid is specified in message -> To a specific partition 
		- If no partitionid specified -> Should be based on hash value of key and total number of functions
		- if no partitionid and no key(? wth is a key) -> Round Robin Method which is also a default method
	- After partition is asssigned, writes are made to a partition leader.

- Consumers:
	- Data Subscribers; essentially any application that receive the message
	- Consumers are identified by means of consumer group; each consumer group can subscribe to any number of topic (kinda like user/role group in aws)
	- Kafka performs assignment of partitions to each consumers.
	- Consumers and how partitions are assigned to them:
		- ![](attachments/Pasted%20image%2020240819073020.png)
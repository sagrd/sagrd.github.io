---
date: 2024-08-11
layout: zettel
category: showcase
tags:
  - data-streaming
link: https://www.youtube.com/watch?v=sa1SkPWifBk
title: kafka
article-name: Apache Kafka - Introduction & Architecture
---
- Kafka is distributed streaming message platform
	- [distributed-systems](../distributed-systems/distributed-systems.md) : 
		- Lets say there are the number of processes writing data into a system with certain specification.
			- As the number of processes increase, in order to account for the changes the specification of system should also increase (vertical scaling) which can be extremely costly. They have problem with scalability.
			- Imagine a system gets crashes, all the processes that write data to the system will fail. Similarly all the process that read data from the system will also fail. These system may have availability problem.
			- Additionally, these systems are not fault tolorant ie if one system crashes there is no another system to handle the processes.
			- If we had to restart the system, the data from processes might be corrupted and there is no way to restore the lost data. These systems are not durable.
			- If 10 processes wanted to read a data file at the same time, it cannot be guaranteed. ie very low throughput
		- We'll need to scale system horizontally rather than vertically to resolve these problems. The end result is cluster of computing systems.
	- Streaming message platform:
		- aka Message Bus
			- Why?
				- Lets say there is a source and multiple targets, as the number of targets increase the load on source is naturally going to increase. To account for this if we end of increasing number of source that will definitely increase the number of pipelines (2 to 4). Similarly if target expects response in json file and source is in csv; this can add additional complexity.
			- Solution:
			- ![](attachments/Pasted%20image%2020240811210325.png)
			- All processes that write data (here publishers) into a common system from where processes that read data (here subscribers) feed from.
	
	- What if there are multiple common systems (instead of 1 in above picture) working on a distributed fashion. Thats essentially kafka.
	- 
- Kafka is written in java and scala but has support for several clients: C++, python, etc
- Mainly used for 2 tasks:
	- Real time data pipelines
	- Real time streaming applications
---
date: 2024-08-21
layout: zettel
category: showcase
link: https://www.youtube.com/watch?v=sa1SkPWifBk
tags:
  - data-streaming
article-name: Apache Kafka Series
---
- Installation Summary:
	- Download [[Kafka]], append path variable, symbolic links, etc. 
	- Launch Zookeeper with `zookeeper-server-start`
	- Create Property files for each broker and launch the brokers with `kafka-server-start.sh`
- List all the topics:
	- `kafka-topics.sh --list --zookeeper localhost:2181`
- Create topics
	- `kafka-topics.sh --create --zookeeper localhost:2181 --topic first-topic --partitions 2 --replication-factor 3`
- Get Metadata information for each topic
	- `kafka-topics.sh --list --zookeeper localhost:2181 --topic first-topic --describe`
	- ![](attachments/Pasted%20image%2020240821093931.png)
- Create Simple Kafka Control Producer
	- `kafka-console-producer.sh --broker-list localhost:9092,localhost:9093 --topic first-topic` here, localhosts are address of broker, good idea to pass multiple to ensure resilance
	- `>> I am passing this message which we will read from consumer`
- Create Kafka Console Consumer
	- `kafka-console-consumer.sh --bootstrap-server localhost:9092,localhost:9093 --topic first-topic --from-beginning --group first-consumer`
		- `--from-beginning`: get all the message, alternative to specifying offset.
		- `>> I am passing this message which we will read from consumer`
- Zookeeper admin server
	- Allows monitering via http interface
		- `localhost:9090/commands/watches`
		- `localhost:9090/commands/stats`
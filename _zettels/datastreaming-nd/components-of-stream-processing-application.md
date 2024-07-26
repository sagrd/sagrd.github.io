---
date: 2024-03-11
layout: zettel
category: show
tags:
  - data-streaming
---
- The components of [stream-processing](glossary/stream-processing.md) application includes
	- data store - this may look like a message queue (eg: kafka) or SQL store (eg: Apache Cassendra)
		- Its responsible for holding all immutable events data in the system.
		- Should guarantee that data is ordered according to created time
		- Should guarantee that data is produced to [consumers](glossary/consumers.md) in the order that is was produced
	- Part responsible for [stream-processing](glossary/stream-processing.md) calculation:
		- These frameworks sit downstream of data store
		- Example of these include:
			- Kafka Streams
			- Apache Flink
			- - Confluent KSQL, etc
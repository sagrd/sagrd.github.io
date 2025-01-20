---
date: 2024-08-27
layout: zettel
category: showcase
tags:
  - data-streaming
title: data management in kafka topics
---
- **Data retention** determines how long Kafka stores data in a topic.
    - [The `retention.bytes`, `retention.ms` settings control retention policy](https://kafka.apache.org/documentation.html#topicconfigs)
- When data _expires_ it is deleted from the topic.
    - [This is true if `cleanup.policy` is set to `delete`](https://kafka.apache.org/documentation.html#topicconfigs)
- Retention policies may be time based. Once data reaches a certain age it is deleted.
    - [The `retention.ms` setting controls retention policy on time](https://kafka.apache.org/documentation.html#topicconfigs)
- Retention policies may be size based. Once a topic reaches a certain age the oldest data is deleted.
    - [The `retention.bytes` setting controls retention policy on time](https://kafka.apache.org/documentation.html#topicconfigs)
- Retention policies may be both time- and size-based. Once either condition is reached, the oldest data is deleted.
- Alternatively, topics can be **compacted** in which there is no size or time limit for data in the topic.
    - [This is true if `cleanup.policy` is set to `compact`](https://kafka.apache.org/documentation.html#topicconfigs)
- Compacted topics use the message key to identify messages uniquely. If a duplicate key is found, the latest value for that key is kept, and the old message is deleted.
- Kafka topics can use compression algorithms to store data. This can reduce network overhead and save space on brokers. Supported compression algorithms include: lz4, ztsd, snappy, and gzip.
    - [`compression.type` controls the type of message compression for a topic](https://kafka.apache.org/documentation.html#topicconfigs)
- Kafka topics should store data for one type of event, not multiple types of events. Keeping multiple event types in one topic will cause your topic to be hard to use for downstream consumers.
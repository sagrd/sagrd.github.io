---
date: 2024-08-20
layout: zettel
category: show
tags:
  - data-streaming
title: message batching in kafka clients library
---
- When kafka client library sends messages the messages are technically not sent individually, instead they are grouped and sent to kafka brokers. This groups of messages are known as batches
- Client library do this mainly for performance reasons: in high throughput applications sending every message as it is produced can lead to significant amount of networking overhead. The count, frequency and quantity of data sent in these batches can be customizable.
- For example: confluent kafka library sends the batch if any one of these conditions are met:
	- first 10000 messages are queued up to be sent
	- a half second of time has elapsed since last batch of messages were sent
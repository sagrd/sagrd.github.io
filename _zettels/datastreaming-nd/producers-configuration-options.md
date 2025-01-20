---
date: 2024-08-28
layout: zettel
category: show
tags:
  - data-streaming
title: configurating producers in kafka
---
- Producer Configuration Options - Summary
	- All available settings for the `confluent_kafka_python` library can [be found in the librdkafka configuration options](https://github.com/edenhill/librdkafka/blob/master/CONFIGURATION.md). `confluent_kafka_python` uses `librdkafka` under the hood and shares the exact configuration options in this document.
	- It is a good idea to always set the `client.id` for improved logging, debugging, and resource limiting
	- The `retries` setting determines how many times the producer will attempt to send a message before marking it as failed
	- If ordering guarantees are important to your application and you’ve also enabled retries, make sure that you set `enable.idempotence` to true
	- Producers may choose to compress messages with the `compression.type` setting
	    - Options are `none`, `gzip`, `lz4`, `snappy`, and `zstd`
	    - Compression is performed by the producer client if enabled
	    - If the topic has its own compression setting, it must match the producer setting, otherwise the broker will decompress and recompress the message into its configured format.
	    - The `acks` setting determines how many In-Sync Replica (ISR) Brokers need to have successfully received the message from the client before moving on
	    - A setting of `-1` or `all` means that all ISRs will have successfully received the message before the producer proceeds
	    - Clients may opt to set this to 0 for performance reasons
	- The diagram below illustrates how the topic and producer may have different compression settings. However, the setting at the topic level will always be what the consumer sees.
	- ![](attachments/Pasted%20image%2020240828180542.png)
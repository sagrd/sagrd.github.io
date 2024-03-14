---
date: 2024-03-11
layout: zettel
category: 
tags:
  - data-streaming
---
What is stream processing ??
- Stream processing is the act of performing calculations on [stream](stream.md). Here are some of the properties of data stream.
	- The data in stream processing is immutable ie it doesn't change / can't be updated.
	- Another data stream can be placed in the stream that supersedes the previous data entry if necessary.
	- Data sent to stream is usually small - less than 1MB in size
	- However the throughput in data streams could be variable - some receives 1-2 records whereas some stream can receive thousands or tens of thousand.
- Following are examples where stream processing can be used:
	- Finding patterns and meaningful log data in log files from different sources
	- Analyzing streaming user events for web analytics (no. of counts, views, etc)
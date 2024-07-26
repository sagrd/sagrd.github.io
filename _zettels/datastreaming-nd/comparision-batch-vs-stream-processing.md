---
date: 2024-03-11
layout: zettel
category: show
tags:
  - data-streaming
---
- Batch Processing vs [stream-processing](glossary/stream-processing.md) comparison 
	- Batch Processing
		- Usually runs on scheduled basis
		- May take longer time to run and usually stores the result somewhere
		- May analyze all historical records at once
		- Typically work with Mutable data 
	- Streaming Processing:
		- Runs whenever events are generated
		- Typically runs quickly
		- They may emit [event](glossary/event.md) themselves, rather than writing to data store
		- Usually analyzes trends over limited period of time
		- Typically analyzes immutable data
	- Batch and stream processing applications are not mutually exclusive. Batch systems can create events to feed into stream processes and streaming processes can be part of batch analysis.
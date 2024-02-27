---
date: 2024-02-27
layout: zettel
category: flash
tags:
  - geo-distributed
---
Problems and Approaches in geo-distributed systems ???
- low response times(latency) for analytics queries issued across all geo-distributed sites
	- Latency depends heavily on Query Execution Plan
		- [Clarinet](papers/Clarinet.md) - A WAN-aware query optimizer attempts to work on it.
	- There also could be bottlenecks at the runtime
		- [Lube](papers/Lube.md) - a system framework that detects and minimize bottlenecks
	- Data transfer issue across sites & network Performance bottleneck
		- running queries over geo-distributed inputs using the current intra-DC analytics frameworks 
			- also leads to high latency because these frameworks cannot cope with the relatively low and variable capacity of WAN links
			- Better approach: [Iridium](papers/Iridium.md)
		- Running parallel jobs across geo-distributed sites
			- [Tetrium](papers/Tetrium.md)
	- network transfer cost also need to be considered
		- [Kimchi](papers/Kimchi.md) - a network cost aware geo-distributed analytics system

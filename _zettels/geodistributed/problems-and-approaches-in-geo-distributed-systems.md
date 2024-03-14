---
date: 2024-02-27
layout: zettel
category: show
tags:
  - geo-distributed
---
- Problems and Approaches in [[geo-distributed-systems ]] ?? 
	- low response times(latency) for analytics queries issued across all geo-distributed sites
		- Most common approach is loading relevant data to a datacenter and centrally executing it.
			- Not ideal as this is slow and we might need (near) real time analysis
		- Latency depends heavily on Query Execution Plan
			- But query optimizers are not aware 
		- There also could be bottlenecks at the runtime
			- [lube](papers/lube.md) - a system framework that detects and minimize bottlenecks
		- Data transfer issue across sites & network Performance bottleneck
			- running queries over geo-distributed inputs using the current intra-DC analytics frameworks 
				- also leads to high latency because these frameworks cannot cope with the relatively low and variable capacity of WAN links
				- Also Expensive to transfer all data to a site
					- [iridium](papers/iridium.md)- WAN-aware input data and task placement for two-stage MapReduce jobs
					- [clarinet](papers/clarinet.md) - A WAN-aware query optimizer attempts to work on it.
			- Running parallel jobs across geo-distributed sites
				- [tetrium](papers/tetrium.md)
		- network transfer cost also need to be considered
			- [kimchi](papers/kimchi.md) - a network cost aware geo-distributed analytics system

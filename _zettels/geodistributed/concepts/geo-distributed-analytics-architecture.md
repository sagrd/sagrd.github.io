---
date: 2024-02-28
layout: zettel
category: show
tags:
  - geo-distributed
---
- Architecture of [geo-distributed-systems](../geo-distributed-systems.md)
	- There is a central master where queries are submitted; this is for SparkSQL, HiveQL, Pig Latin, etc
	- Query Optimizer at master is responsible for preparing Query Execution plan.
	- There is also a centralized scheduler which places tasks in Nodes
		- placement is based on resource availability and task dependencies (upstream/ downstream, etc) 
		- 
	
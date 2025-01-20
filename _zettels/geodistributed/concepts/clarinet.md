---
date: 2024-02-27
layout: zettel
category: show
tags:
  - geo-distributed
  - article
article-name: "Clarinet: WAN-Aware Optimization for Analytics"
link: https://www.usenix.org/conference/osdi16/technical-sessions/presentation/viswanathan
---
Problem:
- Existing query optimizer do not consider network (heterogenous and variable bandwidth) or [wan-constraints-geo-distributed-systems](../concepts/wan-constraints-geo-distributed-systems.md) when preparing query execution plan 
Intuition:
- Getting WAN aware execution plan requires working with execution layer (of analytical framework) responsible for [[../concepts/task-placement]]  across sites and [[../concepts/tasks-scheduling]]
- Factors affecting latency
	- Choice of join order
	- Optimization of [task-placement](../concepts/task-placement.md) involves moving intermediate data less. So we'd have to consider running time from base task placement.
	- If the data transfer link is used by different application, so we'd also have to consider schedule of network transfer too.
- 
Approach:
- Clarinet solves these problem by taking following approach
	- Generate multiple query plans (with different join order per query)
	- Assign parallelism for each stage for converting these logical plans to physical plans
	- These plans are fed into Clarinet which does task placement and scheduling in network aware fashion
	- Choose plan with smallest run time for execution.
	- 
Implementation:
- For single query WAN Awareness
- For Multiple Contending Queries
	
Conclusion:
- reduces query completion times by 2× compared to using state-of-the-art WAN-aware placement and scheduling
- see also [potential-ideas](../private/potential-ideas.md)
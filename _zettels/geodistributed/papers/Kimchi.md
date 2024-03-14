---
date: 2024-02-29
layout: zettel
category: 
tags:
  - geo-distributed
  - article
article-name: "Kimchi: Network Cost-aware Geo-distributed Data Analytics System"
link: https://www.computer.org/csdl/journal/td/2022/06/09527073/1wzrYSZ16Te
---
- Problem:
	- Data transfer cost across distributed sites should also be considered as its one of the most expensive metrics.

- Approach/Intuition: 
	- Schedules placement of tasks based on data transfer cost, input data size, locations and desired cost performance tradeoff
	- improves cost-aware task placement, a cost-aware task adjustment, and a cost-aware push-based mechanism.

- Implementation:
	- GDA MapReduce models: synchronous barrier and asynchronous push-based shuffle.

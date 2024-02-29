---
date: 2024-02-28
layout: zettel
category: 
tags:
  - distributed-systems
---
How to improve performance of joins with bloom filter:
- We can improve the performance of some joins by pre-filtering one side of a join using a Bloom filter and IN predicate generated from the values from the other side of the join.
- link: https://issues.apache.org/jira/browse/SPARK-32268
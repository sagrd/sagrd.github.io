---
date: 2024-02-12
layout: zettel
category: 
tags:
  - distributed-serverless
---
What are difference between metrics for evaluating performance of [distributed-serverless](distributed-serverless.md) and [distributed-systems](../distributed-systems/distributed-systems.md) based infrastructures
- For server-based systems, metrics include Average JCT, cluster utilization and fairness across jobs; they are inter-job scheduling metrics
- For [distributed-serverless](distributed-serverless.md) systems, inter-job metrics could be problem but we focus on intra-job metrics. More importantly the question is how to use intra-job scheduling policies to optimize associated metrics (JCT and Cost for each individual job)
- See also [inter-and-intra-job-scheduling](inter-and-intra-job-scheduling.md)
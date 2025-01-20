---
layout: post
---
Partitioning, also known as sharding, is essential for handling very large datasets or achieving high query throughput. Each partition operates as a mini-database, allowing data and query load to be distributed across multiple processors, enhancing scalability.

## Introduction
- Partitioning and Replication:
  - Each record belongs to a single partition but can be stored on multiple nodes for fault tolerance.
  - Nodes can store multiple partitions, balancing the load and improving reliability.

- Goals of Partitioning:
  - Distribute data and query load evenly across nodes to avoid hotspots.
  - Unfair or skewed partitioning can lead to inefficiencies and uneven load distribution.

## Basic Partitioning Strategies:
  - Random Assignment:
    - Simple but inefficient for specific item retrieval as all nodes must be queried in parallel.
  - Key Range Partitioning:
    - Assigns continuous key ranges to partitions, facilitating easy scans.
    - Manual or automatic boundary selection is possible, but hot spots can occur with certain access patterns.
  - Hash Partitioning:
    - Utilizes hash functions like MD5 or Murmur3 to distribute data uniformly.
    - Efficient for load distribution but complicates range queries.

## Handling Skewed Workloads and Hot Spots:
  - Complete elimination of hot spots is challenging, but application-level techniques can mitigate their impact.
  - Adding random elements to keys can help distribute writes, though it may complicate reads.

## Partitioning with Secondary Indexes:
  - Secondary indexes complicate partitioning as they don’t map neatly to partitions.
  - Local Indexes:
    - Each partition maintains its own indexes, requiring scatter/gather queries across all partitions.
  - Global Indexes:
    - Constructed to cover all partitions, facilitating efficient reads but complicating and slowing writes.

## Rebalancing Partitions:
  - Hash Mod N:
    - Inefficient as changes in the number of nodes necessitate widespread key reassignments.
  - Fixed Number of Partitions:
    - Pre-define many partitions, distributing them among nodes. Adding new nodes involves reassigning partitions without altering the overall structure.
  - Dynamic Partitioning:
    - Adapts the number of partitions to data volume, starting small and growing as needed. Examples include HBase and MongoDB.
  - Proportional to Nodes:
    - Systems like Cassandra and Ketama make partition count proportional to node count, ensuring stable partition sizes.

## Automatic vs. Manual Rebalancing:
  - Fully automated rebalancing can strain network and node resources, potentially impacting performance.
  - Manual intervention in rebalancing can prevent operational surprises and maintain system stability.

## Request Routing:
  - Client-to-Node Direct Routing:
    - Clients contact any node, which handles or forwards the request.
  - Routing Tier:
    - A partition-aware load balancer directs requests to the appropriate nodes.
  - Partition-Aware Clients:
    - Clients are aware of partition assignments, improving efficiency.
  - Cluster Metadata Coordination:
    - Tools like ZooKeeper manage partition-to-node mappings. Systems like HBase, SolrCloud, Kafka, MongoDB, Cassandra, and Riak use various methods for tracking and updating these mappings.

## Parallel Query Execution:
  - Massively Parallel Processing (MPP) relational databases support sophisticated queries, leveraging partitioning for optimized performance. 

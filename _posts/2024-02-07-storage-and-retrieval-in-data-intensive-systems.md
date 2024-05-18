---
layout: post
---

The Simplest and most efficient write operation is appending to a file.

## Indexing in Databases:
  - Databases doesn't usually index everything by default; manual selection is required.

- Hash Index:
  - Structure: In-memory key-value store mapping keys to byte offsets in the data file.
  - Operations: 
    - New records appended to a fixed-size segment.
    - Background thread merges and compacts segments.
    - Reliability: One thread writes, snapshots of hash map written to disk regularly.
  - Advantages: 
    - Faster sequential writes.
    - Simplified concurrency and crash recovery.
  - Limitations: 
    - Hash table must fit in memory.
    - No support for range queries.

- Log-Structured Merge-Tree (LSM-Tree):
  - Structure: In-memory balanced tree (e.g., AVL, Red-Black) keeping records sorted.
  - Write Operations: Append-only, very fast.
  - Read Operations: 
    - Check memory table first.
    - Then recent file segments in descending order.
  - Crash Resilience: Writes appended to a secondary disk log file.
  - Advantages:
    - Efficient segment merging.
    - No need to index all keys in memory.
    - Records can be grouped and compressed before disk writes.
  - Limitations: 
    - Slow for non-existent keys (Bloom filter can help).

- B-Tree Index:
  - Structure: Most widely used indexing structure.
    - Database broken into fixed-size pages (4 KB).
  - Balance and Depth: Balanced, with depth O(log n).
  - Branching Factor: Typically several hundreds.
  - Crash Resilience: Append-only log file on disk.
  - Concurrency Handling: Uses latches.
  - Optimizations: 
    - Writing modified pages to new locations.
    - Storing key abbreviations.
    - Referencing sibling nodes in leaf layer.

- LSM-Trees vs. B-Trees:
  - LSM-Trees Advantages:
    - Faster writes.
    - Higher write throughput.
    - Better compression.
    - Lower write amplification.
  - LSM-Trees Disadvantages:
    - Slower reads.
    - Compaction may interfere with performance.
    - Less predictable performance.
    - Can consume disk bandwidth and space with un-merged segments.
    - Same key might exist in multiple segments.

- Secondary Indexes:
  - Purpose: Crucial for joins in relational databases.
  - Types: Both B-Trees and LSM-Trees support secondary indexes.

- Clustered Index:
  - Stores all row data within the index.
  - Allows some queries to be answered using the index alone.

- Multi-Column Indexes:
  - Useful for querying several columns simultaneously (e.g., Geo-spatial data).
  - Converts multi-dimensions into a single value.

- Fuzzy Indexes:
  - Helps in querying similar keys when exact key is unknown.
  - Useful in document classification and machine learning.

- In-Memory Databases:
  - Advantages: Much faster, great for small datasets and complex data models (e.g., queues, sets).
  - Disadvantages: Less durable, more expensive.
  - Durability: Needs to write to disk asynchronously.

## Transaction Processing or Analytics?

- Types of Databases:
  - Online Transaction Processing (OLTP): For everyday transactions.
  - Online Analytic Processing (OLAP): For analytics (Data Warehouse).

- Data Warehouses:
  - Purpose: Provide data for business analytics without affecting OLTP performance.
  - Data Transfer:
    - Periodic data dump or continuous updates.
    - Data is transformed before loading into the warehouse.
  - Advantages: 
    - Optimized for analytic access patterns.
    - Typically relational due to SQL’s strength in analytics.

## Column-Oriented Storage

- Data Warehouse Tables:
  - Typically very wide, accessing few columns at a time.
  - More efficient to store each column’s data together.

- Column-Based Datastores:
  - Advantages:
    - Compression benefits from data repetition.
    - Vectorized processing uses CPU cycles efficiently.
  - Disadvantages:
    - Writes are more difficult (in-place updates not possible).
    - Solved by in-memory structures like LSM-Trees, sorted and accumulated before disk writes.

- Materialized Aggregates:
  - Purpose: Cache frequently used aggregated data.
  - Implementation: In relational models, created using materialized views.
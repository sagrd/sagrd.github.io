---
layout: post
---

#### Introduction
- The Challenge of Fault-Tolerant Mechanisms:
  - Implementing fault tolerance is complex and essential for robust systems.
  - Transactions simplify error handling and concurrency issues by grouping reads and writes as a single operation.

- The Concept of Transactions:
  - A transaction is a single unit of execution that either fully succeeds (commit) or fails (abort, rollback).
  - This ensures safety guarantees by allowing applications to ignore certain error scenarios and concurrency issues.

#### ACID Properties:
  - Atomicity:
    - Ensures all-or-nothing execution of transactions. If a fault occurs, partial writes are rolled back.
    - Implemented using logs for crash recovery.
  - Consistency:
    - Ensures data invariants are maintained. Consistency depends on the application's notion of valid states.
  - Isolation:
    - Ensures transactions execute as if they were the only one in the system, avoiding concurrency issues.
    - Implemented using locks to serialize access to objects.
  - Durability:
    - Ensures committed data is not lost, even in case of hardware failure. Achieved through replication or non-volatile storage.

#### Handling Errors and Aborts:
  - Transactions can be safely retried if they abort due to errors.
  - In leaderless replication, the application is responsible for error recovery.
  - Safe retries are a core benefit of transactional aborts.

#### Weak Isolation Levels:
  - Read Committed:
    - Guarantees no dirty reads and no dirty writes.
    - Uses row-level locks to prevent dirty writes.
    - Handles dirty reads by maintaining old and new values during transactions.
  - Snapshot Isolation and Repeatable Read:
    - Each transaction works with a consistent snapshot, avoiding temporal inconsistencies.
    - Uses Multi-Version Concurrency Control (MVCC) to keep multiple committed versions of an object.
    - Prevents dirty writes using write locks.

#### Concurrency Issues and Solutions:
  - Preventing Lost Updates:
    - Atomic Write Operations:
      - Avoid read-modify-write cycles with atomic updates (e.g., SQL `UPDATE` statements).
    - Explicit Locking:
      - Applications can lock objects to ensure update consistency.
    - Automatically Detecting Lost Updates:
      - Transaction managers can detect and abort transactions with lost updates.
  - Compare-and-Set:
    - Ensures updates only if the current value matches the expected value.

#### Write Skew and Phantoms:
  - Write Skew:
    - Occurs when concurrent transactions read the same data and then update it, leading to inconsistent states.
    - Mitigated by explicit locking or serializable isolation.
  - Phantoms:
    - Prevented by predicate locks or index-range locks to ensure new objects do not violate existing queries.

#### Serializable Isolation:
  - Serial Execution:
    - Transactions are executed one at a time, ensuring no concurrency issues but limiting throughput.
  - Two-Phase Locking (2PL):
    - Transactions acquire and hold locks until completion, preventing race conditions but potentially causing deadlocks and slow performance.
  - Serializable Snapshot Isolation (SSI):
    - Combines snapshot isolation with conflict detection to provide full serializability without significant performance penalties.

#### Optimistic vs. Pessimistic Concurrency Control:
  - Pessimistic Concurrency Control:
    - Transactions wait to acquire locks, ensuring safety but reducing concurrency and performance.
  - Optimistic Concurrency Control:
    - Transactions proceed without waiting, with conflicts checked at commit time. Abort and retry if necessary.
  - SSI Performance:
    - SSI allows for concurrent reads and writes, providing better performance compared to 2PL and serial execution.

#### Index Handling in Multi-Version Databases:
  - Indexes point to all versions of an object, filtering out versions not visible to the current transaction.
  - Ensures efficient querying while maintaining consistency.

#### Advanced Techniques for Transaction Management:
  - Stored Procedures:
    - Encapsulate transactions for faster execution, but come with debugging and version control challenges.
  - Partitioning:
    - Distributes transactions across multiple partitions, coordinating across partitions for multi-partition transactions.

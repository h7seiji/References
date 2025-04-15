# Databases

## CAP Theorem

The CAP theorem states that in distributed systems, you can have at most two out of three desirable properties simultaneously: Consistency, Availability, and Partition tolerance.
This fundamental principle helps system designers understand the trade-offs they must make when building distributed databases and applications.

### Consistency

- Ensures all clients see the same data regardless of which node they connect to
- Requires instant replication across all nodes for successful writes
- Example: Banking systems requiring exact account balances

### Availability

- Guarantees valid responses to client requests, even when nodes fail
- Every working node must return a response without exception
- Example: E-commerce platforms needing 24/7 operation

### Partition tolerance

- Ensures system functionality despite network communication breakdowns
- Required for distributed systems due to inevitable network failures
- Allows continued operation even when nodes lose contact

### CP Systems (Consistency + Partition tolerance)

- Example: MongoDB
- Prioritizes consistency over availability during partitions
- May temporarily reject writes to maintain consistency

### AP Systems (Availability + Partition tolerance)

- Example: Cassandra
- Maintains availability but may sacrifice consistency
- Provides eventual consistency through reconciliation mechanisms

## ACID

- Atomicity: All or nothing
- Consistency: Preserving database invariants
- Isolation: Concurrent transactions are isolated from each other
- Durability: Data is persisted after transaction is committed even in a system failure

## Scaling

- Indexing: Check the query patterns of your application and create the right indexes.
- Materialized Views: Pre-compute complex query results and store them for faster access.
- Denormalization: Reduce complex joins to improve query performance.
- Vertical Scaling: Boost your database server by adding more CPU, RAM, or storage.
- Caching: Store frequently accessed data in a faster storage layer to reduce database load.
- Replication: Create replicas of your primary database on different servers for scaling the reads.
- Sharding: Split your database tables into smaller pieces and spread them across servers. Used for scaling the writes as well as the reads.

## Indexes

Used for the purpose of speeding up reads conditioned on the value of a specific key.
Slows down database writes.

### LSM Trees + SSTables

- Writes first go to a balanced binary search tree in memory
- Tree flushed to a sorted table on disk when it gets too big
- Can binary search SSTables for the value of a key
- If there are too many SSTables they can be merge together (old values of keys will be discarded)

Pro: Fast writes to memory
Con: May have to search many SSTables for value of key

### B-Trees

- A binary tree using pointers on disk
- Writes iterate through the binary tree and either overwrite the existing key value or create a new page on disk and modify the parent pointer to the new page

Pro: Faster reads, know exactly where key is located
Con: Slow writes to disk instead of memory

## Replication

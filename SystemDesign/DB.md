# Databases

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

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

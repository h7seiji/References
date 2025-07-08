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

The process of having multiple copies of data in order to make sure that if a database goes down the data isn't lost

- Single leader replication
  - All writes go to one database, reads come from any database
  - Useful to ensure that there are no data conflicts, all writes go to one node
- Multi leader replication
  - Writes can go to a small subset of leader databases, reads can come from any database
  - Balanced approach between write throughput and write conflicts
- Leaderless replication
  - Writes can go to all databases, reads come from all databases
  - Useful for increasing write throughput at the cost of potential write conflicts

## Choosing a Database

### SQL

- Relational/Normalized data - changes to one table may require changes to others
  - E.g. adding an author and their books to different tables on different nodes
  - May require two phase commit (Expensive)
- Have transactional (ACID guarantees)
  - Excessively slow if you don't need them (due to two phase locking)
- Typically use B-trees
  - Better for reads than writes in theory

Conclusion : When correctness is of more importance than speed - E.g. banking applications, job scheduling

### MongoDB

- Document data model (NoSQL)
  - Data is written in large nested documents, better data locality (if you choose to organize your data in a way that takes advantage of this) - but denormalized
- B-Trees and Transactions supported

Conclusion: Good if you want SQL like guarantees on data with more flexibility via the document model

### Cassandra

- Wide column data store (NoSQL), has a shard key and a sort key
  - Allow for flexible schemas, ease of partitioning
- Multileader/Leaderless replication (configurable)
  - Super fast writes, albeit uses last write wins for conflict resolution
  - May clobber existing writes if they were not the winner of LWW
- Index based off of LSM tree and SSTables
  - Fast writes

Conclusion: Great for applications with high write volume, consistency is not as important, all writes and reads go to the same shard (no transactions) - E.g. chat application

### HBase

- Wide column data store (NoSQL), has a shard key and a sort key
  - Allow for flexible schemas, ease of partitioning
- Single leader replication
  - Built on top of hadoop, ensures data consistency and durability
  - Slower than leaderless replication
- Index based off of LSM tree and SSTables
  - Fast writes
- Column oriented storage
  - Column compression and increased data locality within columns of data

Conclusion: Great for applications that need fast column reads - E.g. Multiple thumbnails of a youtube video, sensor readings

### Neo4j/AWS Neptune

- Graph database
  - As opposed to just using a SQL database under the hood with relations to represent nodes and edges, actually has pointers from one address on disk to another for quicker lookups
  - The former is bad because reads become slower proportional to the size of the index (O log n to binary search), but using direct pointer is O(1)

Conclusion: Only useful for data naturally represented in graph formats - E.g. Map data, friends on social media

### TimeScaleDB/Apache Druid

- Time series database
  - Use LSM trees for fast ingestion, but break table into many small indexes by both ingestion source and timestamp
  - Allows for placing the whole index in CPU cache for better performance, quick deletes of whole index when no longer relevant (as opposed to typical tombstone method)

Conclusion: Very niche but serve their purpose very well - E.g. great for sensor data, metrics, logs, where you want to read by the ingestor and range of timestamp

### VoltDB

- SQL but completely in memory, single threaded execution for no locking
- Expensive and only allows for small datasets

### Google Spanner

- SQL, uses GPS clocks in data center to avoid locking by using timestamps to determine order of writes
- Very expensive

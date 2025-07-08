# Apache Cassandra

## Key Features

- Wide column data store (NoSQL), has a shard key and a sort key
  - Allow for flexible schemas, ease of partitioning
- Multileader/Leaderless replication (configurable)
  - Super fast writes, albeit uses last write wins for conflict resolution
  - May clobber existing writes if they were not the winner of LWW
- Index based off of LSM tree and SSTables
  - Fast writes

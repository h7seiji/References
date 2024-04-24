# Elasticsearch

To perform full-text search, ElasticSearch keeps a large amount of data in RAM and builds complex indices.

## Use-cases

- Search system
- Real-time data analysis pipeline
- Recommendations system

## When not to use ElasticSearch

- ACID Compliance
- When you need complex joins
- Small dataset or simple query needs

## Nodes

Individual Elasticsearch processes.

Usually, you’d run a single Elasticsearch process per machine, so it's easier to think of them as individual servers. Each of these processes is running in isolation from others and is only connected via a common network. Elasticsearch generally runs as a large-scale distributed system, which means you’d typically be running multiple machines(or nodes).

## Clusters

A Cluster is more than a sum of its parts; it isn’t just a certain number of nodes running in isolation. Instead, the nodes are aware that they are part of a cluster and talk to each other when performing different operations.

An ElasticSearch cluster has a huge number of responsibilities, such as storing documents, searching for these documents, performing different analytical and aggregational tasks, backing up data, etc. It also has to manage itself, such as ensuring which nodes are healthy and which are not, deciding which document goes to which node, etc. So, in any significant-sized cluster, it’s important to have distinct nodes for different domains of operations.

The nodes storing data and searching can be “data” nodes, and the node performing more administrative tasks can be called a “master” node.

## Indexes and Documents

Documents are simple JSON objects that you store in ElasticSearch. They are synonymous to rows in a relational database or a single document in MongoDB.

Indexes are collections of similar documents. They are synonymous with tables in relational databases(where every row is a single item), and collections in MongoDB.

## Shards

Documents in an index are divided into multiple shards. Each shard stores a certain subset of the documents of the index.

Shards live in different data nodes across our cluster.

The distribution of these documents into multiple shards gives you multiple advantages:

- Searches can be parallelized.
- Other queries, such as inserting documents(called indexing in Elasticsearch) or retrieving documents by a specific ID, would be distributed among all the nodes.

### Primary, Replica, and Distinct Shards

Replica shards are shards that simply store the same documents that the primary shard it is associated with stores. So a single node failure would not lead to the unavailability of data.

Distinct shard is simply a term used to group the same primary and replicas together.

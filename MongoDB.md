# MongoDB

## OpenSSL CA Certificate for Testing

- <https://www.mongodb.com/docs/manual/appendix/security/appendixA-openssl-ca/>

- [Generate self-signed SSL](Security.md#ssl)

## Transactions

- Transactions can only be used in Replica Sets

## Replica Set

- Data Bearing Nodes: A replica set contains several data bearing nodes and optionally one arbiter node. Of the data bearing nodes, one and only one member is deemed the primary node, while the other nodes are deemed secondary nodes.
- Primary Node: The primary node receives all write operations1. It records all changes to its data sets in its operation log, i.e., oplog.
- Secondary Nodes: The secondary nodes replicate the primary’s oplog and apply the operations to their data sets such that the secondaries’ data sets reflect the primary’s data set. If the primary is unavailable, an eligible secondary will hold an election to elect itself the new primary.
- Arbiter Node: In some circumstances, you may choose to add a mongod instance to a replica set as an arbiter. An arbiter participates in elections but does not hold data (i.e., does not provide data redundancy).

# System Design Interview Patterns

<https://www.youtube.com/watch?v=iYIjJ7utdDI>

## Contending Updates

Many writes to the same key, such that they conflict with one another

Examples: Distributed counter, order inventory on popular products

### Contending Updates Solutions

- Writes to the same database, use locking (naive solution, too slow)
- Multiple database leaders, eventual convergence via automatic merging
- Stream processing
  - Each event can go in a log based message broker, and processed in small batches

## Derived Data

Need to keep two datasets in sync with one another

Example: Global secondary indexes, data transformations on slow database which accepts writes to faster view that is read optimized

### Derived Data Solutions

- Two phase commit (naive, slows down writes but may be unavoidable)
- Change data capture
  - When updating one database, sink its changes into a log based message broker, and use a stateful consumer to enrich the data and sink it to another view
  - Avoids an expensive write, but means the derived dataset is eventually consistent with the original

## Fan Out

Deliver data at write time directly to multiple interested parties to avoid expensive read queries or many active connections on receiving devices

Example: Push notifications, news feed, mutual friends lists, stock price delivery

### Fan Out Solutions

- Synchronous delivery to every interested party (naive, request will time out)
- Asynchronous delivery via stream processing
  - Sink messages to log based message broker, in consumer logic figure out all parties that are interested, and send to them accordingly

### Fan Out Problems

In the prior solution, we are prone to a "popular message" problem. If too many users are interested in the message, it becomes very expensive to send it to all of them.

Instead, we opt for a "hybrid approach".

The majority of messages are delivered directly to destination caches asynchronously.

If the stream consumer deems a message has too many interested parties, it can also place it in a dedicated "popular message cache" that users can poll from.

## Proximity Search

Find close items in a database to you

Examples: Uber driver search, Doordash, Yelp, AirBnb

### Proximity Search Solutions

- Build indexes on latitude and longitude (naive, too slow)
- Use a geospatial index
  - Data likely will need to be partitioned, use bounding boxes as partition methodology
  - Certain geographic areas much more popular than other, shards should have even amount of load, not necessarily geographic coverage

## Job Scheduling

Run a series of tasks on one worker in a cluster

Examples: Build a job scheduler, Netflix/Youtube video upload encoding

### Job Scheduling Solutions

- Round robin jobs into log based message broker partitions (naive)
- In memory message broker delivering messages round robin to workers

## Aggregation

Distributed messages that need to be aggregated by some key or time

Examples: Metrics/logs, job scheduler completion messages, data enrichment

### Aggregation Solutions

- Write everything to a distributed database, run batch job (naive, slow results)
- Stream processing, all messages go into a log based message broker partition based on their aggregation key
  - Stream processing consumer frameworks handle fault tolerance for us

## Idempotence

You do not want to see the output of your task more than once

Examples: One time execution in job scheduler, confirmation emails to users

### Idempotence Solutions

- Two phase commit (naive, slow)
  - Ensures task is marked as completed from one data source at the same time it is performed
- Idempotency keys
  - Store a unique ID for the task and check if we've seen it before for all incoming tasks
  - If reaching an external service can send task ID and external service can reject if it has seen before (fencing tokens)

## Durable Data

You have data that absolutely cannot be lost once written

Examples: Financial transactions

### Durable Data Solutions

- Synchronous replication (naive, if any replica fails no writes can be made)
- Distributed consensus
  - Can tolerate node failures and still proceed
  - Fairly slow for reads and writes, so using change data capture to derive read optimized data views can be very beneficial here

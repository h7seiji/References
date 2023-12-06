# System Design

https://github.com/donnemartin/system-design-primer
https://tianpan.co/notes/2016-02-13-crack-the-system-design-interview
https://www.hiredintech.com/system-design/

## Recipe

- Step 1: Outline use cases, constraints, and assumptions
- Step 2: Create a high level design
- Step 3: Design core components
- Step 4: Scale the design

## Concepts

- Performance vs scalability

  - If you have a performance problem, your system is slow for a single user.
  - If you have a scalability problem, your system is fast for a single user but slow under heavy load.

- Latency vs throughput

  - Latency is the time to perform some action or to produce some result.
  - Throughput is the number of such actions or results per unit of time.

- Availability vs consistency

  - CAP theorem
  - Consistency - Every read receives the most recent write or an error
  - Availability - Every request receives a response, without guarantee that it contains the most recent version of the information
  - Partition Tolerance - The system continues to operate despite arbitrary partitioning due to network failures
  - Networks aren't reliable, so you'll need to support partition tolerance. You'll need to make a software tradeoff between consistency and availability.
  - CP - consistency and partition tolerance
    - Waiting for a response from the partitioned node might result in a timeout error. CP is a good choice if your business needs require atomic reads and writes.
  - AP - availability and partition tolerance
    - Responses return the most readily available version of the data available on any node, which might not be the latest. Writes might take some time to propagate when the partition is resolved.
    - AP is a good choice if the business needs to allow for eventual consistency or when the system needs to continue working despite external errors.

- DNS

  - NS record (name server) - Specifies the DNS servers for your domain/subdomain.
  - MX record (mail exchange) - Specifies the mail servers for accepting messages.
  - A record (address) - Points a name to an IP address.
  - CNAME (canonical) - Points a name to another name or CNAME (example.com to www.example.com) or to an A record.

- CDN

  - Push CDNs
  - Pull CDNs

- Load Balancer

  - Random
  - Least loaded
  - Session/cookies
  - Round robin or weighted round robin
  - Layer 4
  - Layer 7

- Reverse proxy (web server)

  - A reverse proxy is a web server that centralizes internal services and provides unified interfaces to the public.

- DB

  - Relational database management system (RDBMS)
    - Structured data
    - Strict schema
    - Relational data
    - Need for complex joins
    - Transactions
    - Clear patterns for scaling
    - More established: developers, community, code, tools, etc
    - Lookups by index are very fast
  - NoSQL
    - Semi-structured data
    - Dynamic or flexible schema
    - Non-relational data
    - No need for complex joins
    - Store many TB (or PB) of data
    - Very data intensive workload
    - Very high throughput for IOPS

- Cache

  - Client caching
  - CDN caching
  - Web server caching
  - Database caching
  - Application caching

- Asynchronism

  - Message queues
  - Task queues
  - Back pressure

- Communication

  - OSI Layer Model
    - Application
    - Presentation
    - Session
    - Transport
    - Network
    - Data Link
    - Physical
  - HTTP
  - TCP
    - You need all of the data to arrive intact
    - You want to automatically make a best estimate use of the network throughput
  - UDP
    - You need the lowest latency
    - Late data is worse than loss of data
    - You want to implement your own error correction
  - RPC
    - RPC is focused on exposing behaviors. RPCs are often used for performance reasons with internal communications, as you can hand-craft native calls to better fit your use cases.
  - REST
    - Identify resources (URI in HTTP) - use the same URI regardless of any operation.
    - Change with representations (Verbs in HTTP) - use verbs, headers, and body.
    - Self-descriptive error message (status response in HTTP) - Use status codes, don't reinvent the wheel.
    - HATEOAS (HTML interface for HTTP) - your web service should be fully accessible in a browser.

- Security
  - Encrypt in transit and at rest.
  - Sanitize all user inputs or any input parameters exposed to user to prevent XSS and SQL injection.
  - Use parameterized queries to prevent SQL injection.
  - Use the principle of least privilege.

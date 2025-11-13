# REST APIs

## CRUD

- POST: Create a new resource.
- GET: Read or retrieve a resource.
- PUT: Update an entire resource.
- PATCH: Partially update a resource.
- DELETE: Remove a resource.
- HEAD: Retrieve headers for a resource without the response body.
- OPTIONS: Discover the allowed methods and communication options for a resource.
- TRACE: Echo back the request for debugging purposes.
- CONNECT: Establish a tunnel to the server, typically for SSL/TLS through a proxy.

## HTTP Status Code

- Informational (100–199)
- Successful (200–299)
- Redirection (300–399)
- Client Error (400–499)
- Server Error (500–599)

- 200 OK: Successful GET request.
- 201 Created: Resource created successfully (POST).
- 204 No Content: DELETE request successful, no response body.
- 400 Bad Request: Client error due to invalid input.
- 401 Unauthorized: Authentication required or invalid.
- 403 Forbidden: User lacks access rights.
- 404 Not Found: Resource does not exist.
- 409 Conflict: The request could not be completed due to a conflict with the current resource state.
- 5xx Internal Server Error: The server encountered an error.

## Security

- Authentication and Authorization: You can use API keys, OAuth, and JWT (JSON Web Tokens) to control resource access.
- Rate Limiting: Prevent abuse by restricting the number of requests a client can make within a given time frame.
- Input Validation: Protect against common vulnerabilities like SQL injection and XSS by validating all user inputs.
- HTTPS: Always encrypt data in transit using SSL/TLS to secure communication between clients and servers.
- Encryption at Rest: Encrypt sensitive data stored on the server (e.g., databases and logs) to protect against unauthorized access or breaches.

## Versioning

- URL Versioning: Include the version in the URL (e.g., /api/v1/resource or /api/resource?api-version=1).
- Custom Headers: Use headers like Accept: application/vnd.company.v2+json.

## Pagination

### Limit-Offset Pagination

This method uses two parameters:

- limit: Specifies the number of items per page
- offset: Indicates the starting position

`GET /items?limit=10&offset=20`
This request retrieves 10 items starting from the 21st item.

### Cursor-Based Pagination

This method uses a cursor (often an encoded string) to keep track of the current position.

`GET /items?cursor=eyJpZCI6MjB9`

### Page Number Pagination

This approach uses page numbers and page size.

`GET /items?page=3&size=10`
This retrieves the 3rd page with 10 items per page.

### Keyset Pagination

This method uses a unique key (e.g., ID or timestamp) to fetch the next set of items.

`GET /items?after=1627938391&limit=10`

## Rate Limiting

- Preventing Abuse: Stops malicious or excessive use of the API that could overwhelm the system.
- Managing Resource Allocation: Ensures server resources are shared fairly among all clients.
- Ensuring Fair Usage: Protects against a single client monopolizing API capacity.

### Algorithm

- Fixed Window Counter: Simple but can lead to uneven traffic distribution.
- Sliding Log: Offers precise control but may be resource-intensive.
- Sliding Window Counter: Balances precision and efficiency.
- Token Bucket: Allows for traffic bursts while maintaining a long-term rate limit.

## Idempotency

Idempotency ensures that multiple identical requests have the same effect as a single request. For example:

- GET, DELETE, PUT, HEAD, OPTIONS, and TRACE are idempotent.
- POST is indeed not idempotent.

While PATCH is sometimes considered non-idempotent, its idempotency depends on the implementation.

Idempotency is crucial in distributed systems to handle retries without unintended side effects.

The importance of idempotency extends beyond just handling retries in distributed systems:

- Reliability in Distributed Systems: Idempotency allows for safe retries in case of network failures or timeouts, ensuring consistency across distributed components.
- Data Consistency: It prevents unintended side effects from duplicate requests, maintaining data integrity.
- Simplified Error Handling: Clients can safely resend requests without worrying about adverse effects, simplifying error handling logic.
- Fault Tolerance: Idempotent operations improve system resilience by allowing automatic retries in case of failures.
- Concurrency Control: In multi-user environments, idempotency helps minimize conflicts and provides more robust concurrency control.
- Predictability: Systems built with idempotent operations are often more predictable, simplifying testing and maintenance.

## Performance

- Client-Side Caching: Use headers like Cache-Control and ETag to reduce redundant requests.
- Server-Side Caching: Cache frequently accessed data in-memory with tools like Redis or Memcached.
- CDN Caching: Distribute cached content geographically to reduce latency.
- Distributed Caching: Store data across multiple nodes for improved scalability and fault tolerance.
- Database Query Result Caching: This reduces the load on the database and improves response times.
- Database Query Optimization: Focus on optimizing database queries through proper indexing, query analysis, and efficient join operations. Sometimes, a lot of performance gets wasted at the persistence layer.
- Connection Pooling: Reuse database or HTTP connections to avoid the overhead of establishing new connections repeatedly.
- Efficient Data Serialization: You can consider binary formats like Protocol Buffers for faster serialization and deserialization.
- Content Compression: Use HTTP compression (e.g., Gzip or Brotli) to reduce payload size, improving response times for large responses.

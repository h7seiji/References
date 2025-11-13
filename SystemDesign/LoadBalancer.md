# Load Balancer

## HTTP(s) Load Balancer

1. A forwarding rule directs incoming requests to a target HTTP proxy.
2. The target HTTP proxy checks each request against a URL map to determine the appropriate backend service for the request.
3. The backend service directs each request to an appropriate backend based on serving capacity, zone, and instance health of its attached backends. The health of each backend instance is verified using an HTTP health check. If the backend service is configured to use an HTTPS or HTTP/2 health check, the request will be encrypted on its way to the backend instance.
4. Sessions between the load balancer and the instance can use the HTTP, HTTPS, or HTTP/2 protocol. If you use HTTPS or HTTP/2, each instance in the backend services must have an SSL certificate.

## L4 (Transport Layer) Load Balancing

- Works purely at the network/transport layer.
- Balances connections, not individual HTTP requests.
- Doesn’t look inside the packet — so it can’t do routing by path or host.
- Very fast and simple — low overhead, low latency.

### Use L4 when

- You just need to distribute traffic evenly across identical servers.
- Your services speak a non-HTTP protocol (e.g., gRPC, TCP sockets, Redis, game servers).
- You want ultra-low latency and minimal processing overhead.

## L7 (Application Layer) Load Balancing

- Operates at the HTTP (application) layer.
- Can inspect and make routing decisions based on:
- URL paths (/api/v1/users → User service)
- Hostnames (multi-tenant systems)
- Headers (e.g. Authorization, Content-Type)
- Cookies or request method
- Can inject or rewrite headers, do caching, compression, authentication, rate limiting, etc.

### Use L7 when

- You have multiple microservices behind one entry point.
- You need path-based or host-based routing.
- You want built-in observability or security controls.
- You’re building a public-facing API or multi-tenant web app.

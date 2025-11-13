# API Gateway

<https://www.redhat.com/en/topics/api/what-does-an-api-gateway-do>

An API gateway is a piece of software that intercepts API calls from a user and routes them to the appropriate backend service.

- Load Balancing
- Routing
- Authentication
- SSL Termination
- Rate Limiting

## Traffic management

API gateways throttle and manage traffic through various mechanisms designed to control the rate and volume of incoming requests and ensure optimal performance and resource utilization.

- Rate limiting policies specify the maximum number of requests allowed within a certain time period (e.g., requests per second, minute, hour) for each client or API key, protecting backend services from overload.
- Request throttling policies define rules and limits for regulating request traffic, such as maximum request rates, burst allowances, and quotas.
- Concurrency control policies specify the maximum number of concurrent connections or requests that can be handled simultaneously by the backend servers.
- Circuit breaking policies monitor the health and responsiveness of backend servers and temporarily block or redirect traffic away from failing or slow services to prevent cascading failures and maintain overall system stability.
- Dynamic load balancing from API gateways continuously monitors server health and adjusts traffic routing in real-time to handle spikes in demand, minimize response times, and maximize throughput.

## Steps

Step 1 - The client sends an HTTP request to the API gateway.
Step 2 - The API gateway parses and validates the attributes in the HTTP request.
Step 3 - The API gateway performs allow-list/deny-list checks.
Step 4 - The API gateway talks to an identity provider for authentication and authorization.
Step 5 - The rate limiting rules are applied to the request. If it is over the limit, the request is rejected.
Steps 6 and 7 - Now that the request has passed basic checks, the API gateway finds the relevant service to route to by path matching.
Step 8 - The API gateway transforms the request into the appropriate protocol and sends it to backend microservices.
Steps 9-12: The API gateway can handle errors properly, and deals with faults if the error takes a longer time to recover (circuit break). It can also leverage ELK (Elastic-Logstash-Kibana) stack for logging and monitoring. We sometimes cache data in the API gateway.

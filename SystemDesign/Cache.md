# Cache

## CDN

A Content Delivery Network (CDN) is a network of interconnected servers strategically positioned across different geographical locations that accelerates webpage loading for data-heavy applications.
Think of it as a distributed network of "content warehouses" - instead of having one central warehouse that everyone must visit, you have smaller warehouses placed closer to your customers.

### How CDNs Work

When a user visits a website, data typically has to travel across the internet from the server to reach their computer.
If the user is far from the server, this creates significant latency issues, especially for large files like videos or images.
CDNs solve this problem by storing copies of your website content on servers geographically closer to your users.

### How CDNs Improve Performance

- Reduced Latency
  - Content is served from servers closer to users
  - Decreases communication time between websites and users
  - Improves overall website responsiveness
- Bandwidth Optimization
  - Reduces bandwidth costs by minimizing direct requests to origin servers
  - Optimizes server resource utilization
  - Distributes traffic efficiently across multiple locations
- Improved Availability
  - Handles high volumes of concurrent visitors
  - Provides redundancy if one server goes offline
  - Ensures uninterrupted service delivery
- Enhanced Security
  - Protects against DDoS attacks by distributing traffic across multiple servers
  - Reduces the impact of traffic spikes on origin servers
  - Acts as an additional security layer

## Cache Invalidation and cache consistency

- TTL
- Monitoring
- Polaris

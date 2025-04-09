# Gateways

## NAT Gateway

A NAT (Network Address Translation) Gateway is a managed service that enables outbound internet access for resources in private subnets while preventing unsolicited inbound traffic.

- Acts as an intermediary between private subnets and the internet
- Provides controlled outbound-only internet access
- Automatically scales with traffic demands
- Requires configuration in public subnet with proper routing

### Configuration Requirements

#### Location

- Must be placed in a public subnet
- Needs direct route to Internet Gateway
- Cannot be configured in private subnet

#### Route Table Setup

- Private subnet must route traffic to NAT Gateway
- Public subnet requires route to Internet Gateway
- Proper routing tables ensure correct traffic flow

## Internet Gateway

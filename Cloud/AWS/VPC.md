# VPC

## Security

### Security Groups

A security group controls the traffic that is allowed to reach and leave the resources that it is associated with.
For example, after you associate a security group with an EC2 instance, it controls the inbound and outbound traffic for the instance.

When you create a VPC, it comes with a default security group. You can create additional security groups for a VPC, each with their own inbound and outbound rules.
You can specify the source, port range, and protocol for each inbound rule.
You can specify the destination, port range, and protocol for each outbound rule.

- Operate at the instance level
- Only allow rules (no deny rules)
- Stateful - tracks connection state
- Applies to multiple instances
- Changes take effect immediately

Use Security Groups when:

- You need instance-level security control
- Managing a large number of similar instances
- Requiring stateful inspection
- Need to apply consistent rules across multiple instances

#### Stateful Security

- Key Characteristics
  - Tracks connection state and context
  - Remembers communication history
  - Automatic handling of return traffic
  - Only allow rules (no deny rules)

- Implementation
  - Security Groups operate at instance level
  - Maintains connection state table
  - No rule ordering required
  - Automatic return traffic handling

### Network ACLs

A network access control list (ACL) allows or denies specific inbound or outbound traffic at the subnet level.
You can use the default network ACL for your VPC, or you can create a custom network ACL for your VPC with rules that are similar to the rules for your security groups in order to add an additional layer of security to your VPC.

- Operate at the subnet level
- Support both allow and deny rules
- Stateless - each request evaluated independently
- Applies to all instances in subnet
- Rule ordering is crucial (lower numbers = higher priority)

Use Network ACLs when:

- You need subnet-level security control
- Requiring explicit deny rules
- Need to audit all traffic
- Want to enforce network segmentation

#### Stateless Security

- Key Characteristics
  - Each packet evaluated independently
  - No memory of previous connections
  - Rules processed in numerical order
  - Explicit allow/deny rules required

- Implementation
  - Network ACLs operate at subnet level
  - Support both inbound and outbound rules
  - Rule ordering is crucial (lower numbers = higher priority)
  - Must explicitly allow return traffic

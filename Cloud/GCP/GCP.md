# Google Cloud

- <https://www.thecloudgirl.dev/>
- <https://github.com/priyankavergadia/google-cloud-4-words>

## Projects

Projects are the outermost container and are used to group resources that share the same trust boundary. Many developers map Projects to teams since each Project has its own access policy (IAM) and member list. Projects also serve as a collector of billing and quota details reflecting resource consumption. Projects contain Networks which contain Subnetworks, Firewall rules, and Routes (see below architecture diagrams for illustration).

## Networks

Networks directly connect your resources to each other and to the outside world. Networks, using Firewalls, also house the access policies for incoming and outgoing connections. Networks can be Global (offering horizontal scalability across multiple Regions) or Regional (offering low-latency within a single Region).

## Subnetworks

Subnetworks allow you to group related resources (Compute Engine instances) into RFC1918 private address spaces. Subnetworks can only be Regional. A subnetwork can be in auto mode or custom mode.

- An auto mode network has one subnet per region, each with a predetermined IP range and gateway. These subnets are created automatically when you create the auto mode network, and each subnet has the same name as the overall network.
- A custom mode network has no subnets at creation. In order to create an instance in a custom mode network, you must first create a subnetwork in that region and specify its IP range. A custom mode network can have zero, one, or many subnets per region.

## Resources and Access

- Resources are hierarchical
  - Folders
  - Projects
  - Resources
- Resource hierarchy determines policies (Policy Inheritance)

## Storage

### Google Cloud Storage

#### Location Type

- Regional: Good for colocating compute and storage for high performance.
- Multi-Region: Good for serving content to end users and when you want automatic failover.
- Dual-Region: Good for when you need colocated compute and storage and automatic DR.

#### Storage Class

- Standard
- Nearline: For data accessed less than once a month
- Coldline: For data accessed roughly less than once a quarter
- Archive: For long term retention (less than once a year)

Autoclass automatically transitions objects to colder storage classes based on usage patterns

### Move Data

#### GCS Transfer Tools

#### Transfer Service

#### Transfer Appliance

#### BigQuery Data Transfer Service

## Compute Options

### Compute Engine

Like AWS EC2

VM instances

#### Instance Types

- Cost Optimized: E2
- General Purpose: N2, N2D
- ScaleOut Optimized Tau: T2D, T2A
- Compute Optimized: C2, C2D
- Memory Optimized: M1, M2, M3
- Accelerator Optimized: A2

#### Spot VMs

- Super low cost, short-term instances
- 30 seconds notice for preemption

#### Solo-Tenant Nodes

Regular VMs on regular machines, dedicated specifically to your workloads

#### Managed Instance Groups

- Autohealing
- Multi-zone group
- Autoscaling
- Auto-updating
- Stateful

#### Storage Options

- Balanced Persistent Disk: Cost-effective and reliable block storage
- SSD Persistent Disk: Fast and reliable block storage
- Standard Persistent Disk: Efficient and reliable block storage
- Extreme Persistent Disk: Highest performance Persistent Disk block storage option with customizable IOPS
- Hyperdisk Balanced: High performance for demanding workloads with a lower cost
- Hyperdisk Extreme: Fastest block storage option with customizable IOPS
- Hyperdisk Throughput: Cost-effective and throughput-oriented block storage with customizable throughput
- Local SSDs: High performance local block storage
- Cloud Storage Buckets: Affordable object storage

### App Engine

Like AWS Elastic Beanstalk

Serverless orchestration service for deploying web applications

### Cloud Functions

Like AWS Lambda

Serverless functions

2nd Generation runs on Cloud Run with Eventarc

### Cloud Run

Like AWS ECS Fargate, but more streamlined.

Serverless containers

### GKE

Like AWS EKS

Google Kubernetes Engine

## Data

### Cloud Dataproc

Hadoop/Spark on Cloud

### Cloud Dataflow

Stream and batch processing

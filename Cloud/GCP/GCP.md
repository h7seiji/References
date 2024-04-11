# Google Cloud

- <https://www.thecloudgirl.dev/>
- <https://github.com/priyankavergadia/google-cloud-4-words>

## Resources and Access

- Resources are hierarchical
  - Folders
  - Projects
  - Resources
- Resource hierarchy determines policies (Policy Inheritance)

## Storage

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

### App Engine

Like AWS Elastic Beanstalk

Serverless orchestration service for deploying web applications

### Cloud Functions

Like AWS Lambda

Serverless functions

### Cloud Run

Like AWS ECS Fargate, but more streamlined.

Serverless containers

### GKE

Like AWS EKS

Google Kubernetes Engine

## Data

## Cloud Dataproc

Hadoop/Spark on Cloud

## Cloud Dataflow

Stream and batch processing

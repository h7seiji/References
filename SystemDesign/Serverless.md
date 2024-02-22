# Serverless

## Compute Layer

The compute layer of your workload manages requests from external systems, controlling access and verifying that requests are appropriately authorized.
Your business logic will be deployed and started by the runtime environment that it contains.

- AWS Lambda lets you run stateless serverless applications on a managed platform that supports microservice architectures, deployment, and management of execution at the function layer.
- Amazon API Gateway, you can run a fully managed REST API that integrates with Lambda to apply your business logic, and includes traffic management, authorization and access control, monitoring, and API versioning.
- AWS Step Functions orchestrates serverless workflows including coordination, state, and function chaining as well as combining long-running executions not supported within Lambda execution limits by breaking into multiple steps or by calling workers running on Amazon Elastic Compute Cloud (Amazon EC2) instances or on-premises.

## Data layer

The data layer of your workload manages persistent storage from within a system.
It provides a secure mechanism to store the states that your business logic will need.
It provides a mechanism to trigger events in response to data changes.

- Amazon DynamoDB helps you build serverless applications by providing a managed NoSQL database for persistent storage. Combined with DynamoDB Streams, you can respond in near real-time to changes in your DynamoDB table by invoking Lambda functions.
- Amazon Simple Storage Service (Amazon S3), you can build serverless web applications and websites by providing a highly-available key-value store, from which static assets can be served via a Content Delivery Network (CDN), such as Amazon CloudFront.
- Amazon OpenSearch Service (OpenSearch Service) makes it easy to deploy, secure, operate, and scale OpenSearch for log analytics, full-text search, application monitoring, and more. OpenSearch Service is a fully managed service that provides both a search engine and analytics tools.
- AWS AppSync is a managed GraphQL service with real-time and offline capabilities, as well as enterprise-grade security controls that make developing applications simple. AWS AppSync provides a data-driven API and consistent programming language for applications and devices to connect to services such as DynamoDB, OpenSearch Service, and Amazon S3.

## Messaging and streaming layer

The messaging layer of your workload manages communications between components.
The streaming layer manages real-time analysis and processing of streaming data.

- Amazon Simple Notification Service (Amazon SNS) provides a fully managed messaging service for pub/sub patterns using asynchronous Event Notifications and mobile push notifications for microservices, distributed systems, and serverless applications.
- Amazon Kinesis makes it easy to collect, process, and analyze real-time streaming data. With Amazon Kinesis, you can run standard SQL, or build entire streaming applications using SQL.
- Amazon Data Firehose captures, transforms, and loads streaming data into Managed Service for Apache Flink, Amazon S3, Amazon Redshift, and OpenSearch Service, enabling near real-time analytics with existing business intelligence tools.

## User management and identity layer

The user management and identity layer of your workload provides identity, authentication, and authorization for both external and internal customers of your workload’s interfaces.

- Amazon Cognito, you can easily add user sign-up, sign-in, and data synchronization to serverless applications.
- Amazon Cognito User Pools provide built-in sign-in screens and federation with Facebook, Google, Amazon, and Security Assertion Markup Language (SAML).
- Amazon Cognito Federated Identities let you securely provide scoped access to AWS resources that are part of your serverless architecture.

## Edge layer

The edge layer of your workload manages the presentation layer and connectivity to external customers.
It provides an efficient delivery method to external customers residing in distinct geographical locations.

- Amazon CloudFront provides a CDN that securely delivers web application content and data with low latency and high transfer speeds.

## Systems monitoring and deployment

The system monitoring layer of your workload manages system visibility through metrics and creates contextual awareness of how it operates and behaves over time.
The deployment layer defines how your workload changes are promoted through a release management process.

- Amazon CloudWatch, you can access system metrics on all the AWS services you use, consolidate system and application level logs, and create business key performance indicators (KPIs) as custom metrics for your specific needs. It provides dashboards and alerts that can trigger automated actions on the platform.
- AWS X-Ray helps you analyze and debug serverless applications by providing distributed tracing and service maps to easily identify performance bottlenecks by visualizing a request end-to-end.
- AWS Serverless Application Model (AWS SAM) is an extension of AWS CloudFormation that is used to package, test, and deploy serverless applications. The AWS Serverless Application Model CLI can also enable faster debugging cycles when developing Lambda functions locally.

## Deployment approaches

- All-at-once deployments: changes on top of the existing configuration.
- Blue/green deployments: traffic to shift to the new live environment (green) while still keeping the old production environment (blue) warm in case a rollback is necessary.
- Canary deployments: deploying a percentage of requests to new code, and monitoring for errors, degradations, or regressions.

## Lambda version control

- AWS Lambda allows you to publish one or more immutable versions for individual Lambda functions such that previous versions cannot be changed.
- Each Lambda function version has a unique Amazon Resource Name (ARN) and new version changes are auditable as they are recorded in AWS CloudTrail.
- As a best practice in production, customers should enable versioning to use a reliable architecture.
- To simplify deployment operations and reduce the risk of error, Lambda function aliases activate different variations of your Lambda function in your development workflow, such as development, beta, and production.

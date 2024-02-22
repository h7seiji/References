# AWS

## AWS Well-Architected

https://aws.amazon.com/architecture/well-architected/

### Operational Excellence

- Perform operations as code
- Make frequent, small, reversible changes
- Refine operations procedures frequently
- Anticipate failure
- Learn from all operational failures
- Use managed services
- Implement observability for actionable insights

### Security

- Implement a strong identity foundation
- Maintain traceability
- Apply security at all layers
- Automate security best practices
- Protect data in transit and at rest
- Keep people away from data
- Prepare for security events

### Reliability

- Automatically recover from failure
- Test recovery procedures
- Scale horizontally to increase aggregate workload availability
- Stop guessing capacity
- Manage change through automation

### Performance Efficiency

- Democratize advanced technologies
- Go global in minutes
- Use serverless architectures
- Experiment more often
- Consider mechanical sympathy

### Cost Optimization

- Implement cloud financial management
- Adopt a consumption model
- Measure overall efficiency
- Stop spending money on undifferentiated heavy lifting
- Analyze and attribute expenditure

### Sustainability

- Understand your impact
- Establish sustainability goals
- Maximize utilization
- Anticipate and adopt new, more efficient hardware and software offerings
- Use managed services
- Reduce the downstream impact of your cloud workloads

## CI/CD

### Do:

- Treat your infrastructure as code:
  - Use version control for your infrastructure code.
  - Make use of bug tracking/ticketing systems.
  - Have peers review changes before applying them.
  - Establish infrastructure code patterns/designs.
  - Test infrastructure changes like code changes.
- Put developers into integrated teams of no more than 12 self-sustaining members.
- Have all developers commit code to the main branch frequently, with no long-running feature branches.
- Consistently adopt a build system such as Maven or Gradle across your organization and standardize builds.
- Bake security into your code pipeline.
- Have developers build unit tests toward 100% coverage of the code base.
- Ensure that unit tests are 70% of the overall testing in duration, number, and scope.
- Ensure that unit tests are up-to-date and not neglected. Unit test failures should be fixed, not bypassed.
- Treat your continuous delivery configuration as code.
- Establish role-based security controls (that is, who can do what and when):
  - Monitor/track every resource possible.
  - Alert on services, availability, and response times.
  - Capture, learn, and improve.
  - Share access with everyone on the team.
  - Plan metrics and monitoring into the lifecycle.
- Keep and track standard metrics:
  - Number of builds.
  - Number of deployments.
  - Average time for changes to reach production.
  - Average time from first pipeline stage to each stage.
  - Number of changes reaching production.
  - Average build time.
- Use multiple distinct pipelines for each branch and team.

### Don’t:

- Have long-running branches with large complicated merges.
- Have manual tests.
- Have manual approval processes, gates, code reviews, and security reviews.

## Microservices

## Serverless

For reliability, regular testing of failure paths provides you with a better chance of catching errors before they reach production. For performance, starting backward from customer expectations will allow you to design for optimal experience. There are a number of AWS tools to help optimize performance.

For cost optimization, you can reduce waste within your serverless application by right-sizing resources to support traffic demands, and improve value by optimizing your application. For operations, your architecture should strive toward automation in responding to events.

Finally, a secure application will protect your organization’s sensitive information assets and meet any compliance requirements at every layer.

### Design Principles

- Speedy, simple, singular
- Think concurrent requests, not total requests
- Share nothing
- Assume no hardware affinity
- Orchestrate your application with state machines, not functions
- Use events to trigger transactions
- Design for failures and duplicates



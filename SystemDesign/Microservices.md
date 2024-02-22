# Microservices

- Codebase (one codebase tracked in revision control, many deploys) – Each
microservice owns its own codebase in a separate repository and throughout the
lifecycle of the code change.
- Build, release, run (strictly separate build and run stages) – Each microservice
has its own deployment pipeline and deployment frequency. This enables the
development teams to run microservices at varying speeds so they can be
responsive to customer needs.
- Processes (execute the app as one or more stateless processes) – Each
microservice does one thing and does that one thing really well. The
microservice is designed to solve the problem at hand in the best possible
manner.
- Admin processes (run admin/management tasks as one-off processes) – Each
microservice has its own administrative or management tasks so that it functions
as designed.

## Characteristics

- Componentization via services
- Organized around business capabilities
- Products not projects
- Smart endpoints and dumb pipes
- Decentralized governance
- Decentralized data management
- Infrastructure automation
- Design for failure
- Evolutionary design

## Design Patterns

- Aggregator Pattern – A basic service which invokes other services to gather the
required information or achieve the required functionality. This is beneficial when
you need an output by combining data from multiple microservices.
- API Gateway Design Pattern – API Gateway also acts as the entry point for all
the microservices and creates fine-grained APIs for different types of clients. It
can fan out the same request to multiple microservices and similarly aggregate
the results from multiple microservices.
- Chained or Chain of Responsibility Pattern – Chained or Chain of
Responsibility Design Patterns produces a single output which is a combination
of multiple chained outputs.
- Asynchronous Messaging Design Pattern – In this type of microservices
design pattern, all the services can communicate with each other, but they do not
have to communicate with each other sequentially and they usually communicate
asynchronously.
- Database or Shared Data Pattern – This design pattern will enable you to use a
database per service and a shared database per service to solve various
problems. These problems can include duplication of data and inconsistency,
different services have different kinds of storage requirements, few business
transactions can query the data, and with multiple services and de-normalization
of data.
- Event Sourcing Design Pattern – This design pattern helps you to create
events according to change of your application state.
- Command Query Responsibility Segregator (CQRS) Design Pattern – This
design pattern enables you to divide the command and query. Using the common
CQRS pattern, where the command part will handle all the requests related to
CREATE, UPDATE, DELETE while the query part will take care of the
materialized views.
- Circuit Breaker Pattern – This design pattern enables you to stop the process
of the request and response when the service is not working. For example, when
you need to redirect the request to a different service after certain number of
failed request intents.
- Decomposition Design Pattern – This design pattern enables you to
decompose an application based on business capability or on based on the subdomains.


## References

- https://d1.awsstatic.com/whitepapers/DevOps/running-containerized-microservices-on-aws.pdf
- https://docs.aws.amazon.com/pdfs/whitepapers/latest/microservices-on-aws/microservices-on-aws.pdf
- https://medium.com/capital-one-tech/10-microservices-design-patterns-for-better-architecture-befa810ca44e

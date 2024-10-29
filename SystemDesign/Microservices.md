# Microservices

- <https://medium.com/@sylvain.tiset/top-10-microservices-design-patterns-you-should-know-1bac6a7d6218>

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

## Delivering software

- Build, release, run – Engineers adopt a devops culture that allows them to
optimize all three stages.
- Config – Engineers build better configuration management for software due to
their involvement with how that software is used by the customer.
- Dev/prod parity – Software treated as a product can be iteratively developed in
smaller pieces that take less time to complete and deploy than long-running
projects, which enables development and production to be closer in parity.
- Automated provisioning – Operations should be automated rather than
manual. This increases velocity as well as integrates engineering and operations.
- Self-service – Engineers should be able to configure and provision their own
dependencies. This is enabled by containerized environments that allow
engineers to build their own container that has anything they require.
- Continuous Integration – Engineers should check in code frequently so that
incremental improvements are available for review and testing as quickly as
possible.
- Continuous Build and Delivery – The process of building code that’s been
checked in and delivering it to production should be automated so that engineers
can release code without manual intervention.

## Communication between services

- Request/Response – One service explicitly invokes another service by making a
request to either store data in it or retrieve data from it.
- Publish/Subscribe – Event-based architecture where one service implicitly
invokes another service that was watching for an event.

Key Factors:

- Port Binding – Services bind to a port to watch for incoming requests and send
requests to the port of another service. The pipe in between is just a dumb
network protocol such as HTTP.
- Backing services – Dumb pipes allow a background microservice to be
attached to another microservice in the same way that you attach a database.
- Concurrency – A properly designed communication pipeline between
microservices allows multiple microservices to work concurrently. For example,
several observer microservices may respond and begin work in parallel in
response to a single event produced by another microservice.

## Data management design patterns

- Controller – Helps direct the request to the appropriate data store using the
appropriate mechanism.
- Proxy – Helps provide a surrogate or placeholder for another object to control
access to it.
- Visitor – Helps represent an operation to be performed on the elements of an
object structure.
- Interpreter – Helps map a service to data store semantics.
- Observer – Helps define a one-to-many dependency between objects so that
when one object changes state, all of its dependents are notified and updated
automatically.
- Decorator – Helps attach additional responsibilities to an object dynamically.
Decorators provide a flexible alternative to sub-classing for extending
functionality.
- Memento – Helps capture and externalize an object's internal state so that the
object can be returned to this state later.

## Infrastructure automation

- Codebase (one codebase tracked in revision control, many deploys) – Because
the infrastructure can be described as code, treat all code similarly and keep it in
the service repository.
- Config (store configurations in the environment) – The environment should hold
and share its own specificities.
- Build, release, run (strictly separate build and run stages) – One environment
for each purpose.
- Disposability (maximize robustness with fast startup and graceful shutdown) –
This factor transcends the process layer and bleeds into such downstream layers
as containers, virtual machines, and virtual private cloud.
- Dev/prod parity – Keep development, staging, and production as similar as
possible.

## Designing for failure

- Disposability (maximize robustness with fast startup and graceful shutdown) –
Produce lean container images and strive for processes that can start and stop in
a matter of seconds.
- Logs (treat logs as event streams) – If part of a system fails, troubleshooting is
necessary. Ensure that material for forensics exists.
- Dev/prod parity – Keep development, staging, and production as similar as
possible.

## Evolutionary design

- Codebase (one codebase tracked in revision control, many deploys) – Helps
evolve features faster since new feedback can be quickly incorporated.
- Dependencies (explicitly declare and isolate dependencies) – Enables quick
iterations of the design since features are tightly coupled with externalities
- Configuration (store configurations in the environment) – Everything that is
likely to vary between deploys (staging, production, developer environments,
etc.). Config varies substantially across deploys, code does not. With
configurations stored outside code, the design can evolve irrespective of the
environment.
- Build, release, run (strictly separate build and run stages) – Help roll out new
features using various deployment techniques. Each release has a specific ID
and can be used to gain design efficiency and user feedback.

Design patterns:

- Sidecar extends and enhances the main service.
- Ambassador creates helper services that send network requests on behalf of a
- nsumer service or application.
- Chain provides a defined order of starting and stopping containers.
- Proxy provides a surrogate or placeholder for another object to control access to
it.
- Strategy defines a family of algorithms, encapsulates each one, and makes
them interchangeable. Strategy lets the algorithm vary independently from the
clients that use it.
- Iterator provides a way to access the elements of an aggregate object
sequentially without exposing its underlying representation.
- Service Mesh is a dedicated infrastructure layer for facilitating service-to-service
communications between microservices, using a proxy.

## References

- <https://d1.awsstatic.com/whitepapers/DevOps/running-containerized-microservices-on-aws.pdf>
- <https://docs.aws.amazon.com/pdfs/whitepapers/latest/microservices-on-aws/microservices-on-aws.pdf>
- <https://medium.com/capital-one-tech/10-microservices-design-patterns-for-better-architecture-befa810ca44e>

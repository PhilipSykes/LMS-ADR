---
parent: Decisions
nav_order: 6
---

# Use RabbitMQ for message broker

## Context and Problem Statement

After choosing a Service-Oriented Architecture (SOA) for the Advanced Media Library (AML) system, we need to determine how these services will communicate with each other. The system requires communication between various services like Media Management, User Authentication, and Search services.

According to Microsoft's guidance on microservice communication patterns [1], the choice of communication strategy significantly impacts system reliability and scalability.

How should we implement communication between services in our SOA to ensure reliability, scalability, and maintainability?

## Decision Drivers

- Message delivery must be reliable and traceable
- System needs to handle high volumes of inter-service communication
- Communication method should work well with our chosen .NET stack
- Need for asynchronous operations (e.g., updating search index after media changes)

## Considered Options

-Direct HTTP communication between services
-Message broker (RabbitMQ)
-Message broker (Azure Service Bus)

## Decision Outcome

Chosen option: "RabbitMQ". According to Enterprise Integration Patterns [2], message brokers provide the most suitable messaging patterns for SOA, particularly with publish/subscribe capabilities that allow for loose coupling between services.

### Consequences

-Good, because it allows services to communicate without knowing about each other through publish/subscribe increasing security for our app
-Good, because messages will persist even if receiving service is temporarily down adding good data consistency (ACID principles)
Good, because it enables better load handling through message queuing which prevents bottlenecks during high traffic periods[3]
-Bad, because it adds complexity to our infrastructure setup
-Bad, because team needs training in message broker concepts and RabbitMQ specifically

### Confirmation

Initial implementation in sprint 1 took on the form of allocating the message broker as the communication layer between gateway & services. After deliberation & review of our performance targets which were being stifled by this design choice due to latency, this implementation was scaled back to the original plans of purely service to service communication.

## Pros and Cons of the Options

### Direct HTTP communication

-Good, because it's simple to implement initially
-Good, because developers are already familiar with HTTP/REST
-Bad, because it makes asynchronous operations more complex
-Bad, because scaling becomes more difficult as services multiply

### RabbitMQ

-Good, because services can communicate without direct knowledge of each other
-Good, because it handles asynchronous operations naturally
-Good, because failed messages can be retried automatically
-Good, because multiple services can receive the same message via publish/subscribe
-Bad, because it requires setting up and maintaining additional infrastructure
-Bad, because monitoring and debugging is more complex than direct HTTP

### Azure service bus

-Good, because it intergrates better with .NET & blazor due to being part of the same ecosystem.
-Bad, because this it is not free to use compared to other options.
-Bad, because it limits our deployment options to Azure cloud only.

## More Information

During our research, we discovered that a message broker would be more suitable than direct communication for a SOA architecture. RabbitMQ's publish/subscribe model particularly stood out because:

When a media item is updated:

1.Search service needs to update its index
2.Notification service needs to notify relevant users
3.Report service needs to log the change
With publish/subscribe, one message can trigger all these actions without the Media service needing to know about all these dependent services.

### References

[RabbitMQ with .NET](https://www.rabbitmq.com/client-libraries/dotnet) - Official RabbitMQ .NET client documentation.

## Cites

[1]:[Microsoft. "Communication in microservice architecture." Microsoft Learn,](https://learn.microsoft.com/en-us/dotnet/architecture/microservices/architect-microservice-container-applications/communication-in-microservice-architecture) - microsoft guide to communication patterns within microservice style architectures, particularly HTTP & REST communication.

[2]:["Use of messaging brokers", Enterprise Integration Patterns,](https://www.enterpriseintegrationpatterns.com/patterns/messaging/MessageBroker.html) - Explains why and when to use message brokers.

[3]:[Microsoft. "Asynchronous messaging options." Microsoft Learn,](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/messaging) - Microsoft guide to message brokers & overview of Azure service bus.

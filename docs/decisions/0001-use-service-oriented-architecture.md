---
parent: Decisions
nav_order: 1
---

# Use Service-oriented architecture

## Context and Problem Statement

The Advanced Media Library (AML) requires a comprehensive, modern library management system to streamline operations across various access points (in-branch, online, web-mobile app, and telephone services) while serving a large user base across England. The system needs to handle diverse media types, scale for future growth, maintain performance, ensure data integrity, and provide accessibility for all users.

How can we design an architecture that meets these requirements while allowing for maintainability and horizontal scalability?

## Decision Drivers

- Need for a system that can handle 13.4 million users with 10% annual growth i.e. how intuitively scalable is the architecture style
- Performance requirements for rapid search results and quick webpage loading times
- Requirement for centralized management with distributed operations
- Necessity to manage a large volume of diverse media types efficiently
- Need for easy updates and modifications without disrupting the entire system

## Considered Options

- Three-Tier Architecture
- Microservices Architecture
- Service-Oriented Architecture (SOA)

## Decision Outcome

Chosen option: "Service-Oriented Architecture (SOA)", because it provides a balance between the flexibility of microservices and the simplicity of monolithic systems, while meeting our scalability, maintainability, and performance requirements.

### Consequences

- Good, because it has allowed us to explore a new unused architecture type for the team.
- Good, because it has honed our ability to delegate specific sections between the team.
- Good, because its provided the team with better fault isolation & hotfix options throughout development.
- Good, because it allows for easier integration of new technologies and services in the future.
- Bad, because it has resulted in an increased workload developing the various independant services.

## Pros and Cons of the Options

### Confirmation

No current review performed of this ADR.

### Three-Tier Architecture

- Good, because it's simpler to develop and deploy initially.
- Good, because it provides clear separation of concerns between presentation, business logic, and data layers
- Bad, because horizontal scaling is more complex than in service-based architectures.
- Bad, because updates to one part of the system might require redeploying the entire application.
- Bad, because it might not meet our scalability and maintainability requirements in the long term.

### Microservices Architecture

- Good, because it offers the highest level of scalability and flexibility.
- Good, because it allows for independent deployment of services.
- Bad, because it introduces significant complexity in service management and communication.
- Bad, because it might be overkill for our current needs and could lead to over-engineering.
- Bad, because it requires more resources and expertise to implement and maintain effectively.

### Service-oriented Architecture

- Good, because it provides a balance between scalability and manageability.
- Good, because it allows for modular development and deployment of services.
- Good, because it supports our maintainability requirements by allowing updates to individual services.
- Good, because it can meet our performance requirements through optimized service design.
- Neutral, because it introduces some complexity in service communication, but not as much as microservices.
- Bad, because it may require more initial setup compared to a monolithic system.

## More Information

We performed a degree of research from our chosen options to formulate our final decision. links provided below.

### Links

- [Microservices vs. monolithic architecture](https://www.atlassian.com/microservices/microservices-architecture/microservices-vs-monolith) - This article from Atlassian provides a detailed comparison between monolithic and microservices architectures, supporting the pros and cons listed in our ADR.

-[Three-tier architecture](https://www.ibm.com/topics/three-tier-architecture) - comprehensive guide by IBM to three-tier systems.

- [soa-vs-microservices](https://www.ibm.com/think/topics/soa-vs-microservices) - IBM's blog post explains the differences between SOA and microservices, offering insights into why SOA might be a better fit for certain scenarios.

- [Microservices vs. Service-Oriented Architecture](https://www.f5.com/content/dam/f5/corp/global/pdf/ebooks/Microservices_vs_SOA_NGINX.pdf) - NGINX's comparison between microservices and SOA provides additional context for our decision to choose SOA over microservices.

-[Web app architectures](https://learn.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/common-web-application-architectures) - Microsoft guide talking through various facets of web application development including architecture options.

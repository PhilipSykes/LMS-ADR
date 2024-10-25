---
parent: Decisions
nav_order: 5
---

# Use Elasticsearch for search service

## Context and Problem Statement

The Advanced Media Library (AML) system requires a robust and efficient search capability to handle a large volume of diverse media types across multiple branches. The search functionality needs to be fast, scalable, and capable of handling complex queries to provide users with accurate and relevant results. How can we implement a search solution that meets these requirements while integrating seamlessly with our Service-Oriented Architecture?

## Decision Drivers

-Need for fast and efficient search across a large volume of media items
-Scalability to accommodate growing media collection and user base
-Compatibility with our Service-Oriented Architecture
-Support for real-time indexing as new media is added or updated
-Performance under high concurrent user load

## Considered Options

-Elasticsearch
-PostgreSQL full-text search
-Custom-built search solution

## Decision Outcome

Chosen option: "Elasticsearch", because it provides a highly scalable, feature-rich search engine that aligns well with our requirements and integrates smoothly with our Service-Oriented Architecture.

### Consequences

-Good, because it has led to consistently good performance for media searching which is one of our requirements.
-Good, because it works well with our chosen .NET stack through the NEST client
-Good, because index updates can now be performed without downtime
-Bad, because it has added complexity to our deployment and monitoring requirements

### Confirmation

No current review of this ADR yet.

## Pros and Cons of the Options

### Elasticsearch

-Good, because it offers high performance and scalability for large datasets.
-Good, because it provides rich querying capabilities and faceted search.
-Good, because it supports real-time indexing and near real-time search.
-Good, because it has a large community and extensive documentation.
-Good, because it allows for avoidance of a major performance bottleneck on primary database.
-Bad, because it requires additional infrastructure and expertise to manage.
-Bad, because it may introduce complexity in data synchronization with the primary database.

### PostgreSQL full-text search

-Good, because it's built into our existing database system, reducing infrastructure complexity.
-Good, because it provides decent full-text search capabilities for smaller to medium-sized datasets.
-Bad, because it may not scale as well for very large datasets or complex search requirements.
-Bad, because it lacks some advanced features provided by dedicated search engines.
-Bad, because it may lead to bottleneck with performance as query traffic fixed all to primary database.

### Custom-built search solution

-Good, because it could be tailored exactly to our specific needs.
-Good, because it wouldn't introduce dependencies on external systems.
-Good, because it allows for avoidance of a major performance bottleneck on primary database.
-Bad, because it would require significant development time and resources.
-Bad, because it would likely lack the advanced features and optimizations of established search engines.

## More Information

### Links

- [Elasticsearch vs PostgresSQL](https://stackshare.io/stackups/elasticsearch-vs-postgresql) - Comparing features of elasticsearch to postgresSQL.

- [Elasticsearch basics](https://www.elastic.co/guide/en/elasticsearch/reference/current/elasticsearch-intro-what-is-es.html) - Documentation talking through elasticsearch,its features & general use-cases.

- [search systems within micro-services](https://medium.com/@tusharsheth/tech-stack-for-search-system-with-micro-services-architecture-38852c769d87) - Very informative guide regarding search engine implementation along with tech associated, pros & cons.

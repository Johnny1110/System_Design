# System Design Mastery

<br>

---

<br>

> A structured roadmap to master system design interviews for top tech companies (Google, AWS, Microsoft, Netflix, Apple, Meta)

## Goal

Transform from a developer who writes code to an **engineer who designs systems** — understanding the "why" behind every architectural decision.

<br>

## Study Philosophy

1. **Theory First**: Understand concepts deeply before memorizing solutions
2. **Trade-off Thinking**: Every decision has pros and cons — know them
3. **Progressive Complexity**: Build mental models from simple to complex
4. **Practice with Purpose**: Mock interviews with real company-style problems

<br>

---

<br>

## Roadmap Overview

| Phase | Focus |
|-------|-------|
| Phase 1 | Fundamentals & Building Blocks |
| Phase 2 | Core Distributed Systems Concept |
| Phase 3 | Data Systems Deep Dive |
| Phase 4 | Real-World System Designs|
| Phase 5 | Advanced Topics & Mock Interview |

<br>

---

<br>

## Detailed Roadmap

> On going mark: [👈], Already done mark: [💯]


### Phase 1: Fundamentals & Building Blocks

Master the vocabulary and basic components that every system uses.

#### Week 1: Networking & Communication
- [1.1 How the Inte`rnet Works](./phase-1/01-networking/01-how-internet-works.md) 👈
- [1.2 HTTP/HTTPS Deep Dive](./phase-1/01-networking/02-http-https.md)
- [1.3 TCP vs UDP — When to Use What](./phase-1/01-networking/03-tcp-vs-udp.md)
- [1.4 WebSockets & Long Polling](./phase-1/01-networking/04-websockets-long-polling.md)
- [1.5 DNS — The Phone Book of the Internet](./phase-1/01-networking/05-dns.md)

#### Week 2: APIs & Communication Patterns
- [2.1 REST API Design Principles](./phase-1/02-apis/01-rest-api.md)
- [2.2 GraphQL — When and Why](./phase-1/02-apis/02-graphql.md)
- [2.3 gRPC — High Performance Communication](./phase-1/02-apis/03-grpc.md)
- [2.4 API Gateway Pattern](./phase-1/02-apis/04-api-gateway.md)
- [2.5 Rate Limiting & Throttling](./phase-1/02-apis/05-rate-limiting.md)

#### Week 3: Storage Fundamentals
- [3.1 SQL vs NoSQL — The Right Tool for the Job](./phase-1/03-storage/01-sql-vs-nosql.md)
- [3.2 Database Indexing — How and Why](./phase-1/03-storage/02-indexing.md)
- [3.3 ACID vs BASE — Consistency Models](./phase-1/03-storage/03-acid-vs-base.md)
- [3.4 Caching Strategies](./phase-1/03-storage/04-caching.md)
- [3.5 Blob Storage & CDN](./phase-1/03-storage/05-blob-cdn.md)

---

### Phase 2: Core Distributed Systems Concepts

Understand how systems scale and stay reliable.

#### Week 4: Scaling Patterns
- [4.1 Vertical vs Horizontal Scaling](./phase-2/04-scaling/01-vertical-vs-horizontal.md)
- [4.2 Load Balancing — Algorithms & Strategies](./phase-2/04-scaling/02-load-balancing.md)
- [4.3 Database Replication](./phase-2/04-scaling/03-db-replication.md)
- [4.4 Database Sharding / Partitioning](./phase-2/04-scaling/04-sharding.md)
- [4.5 Consistent Hashing](./phase-2/04-scaling/05-consistent-hashing.md)

#### Week 5: Reliability & Fault Tolerance
- [5.1 CAP Theorem — The Fundamental Trade-off](./phase-2/05-reliability/01-cap-theorem.md)
- [5.2 Replication Strategies (Leader-Follower, Multi-Leader, Leaderless)](./phase-2/05-reliability/02-replication-strategies.md)
- [5.3 Consensus Algorithms (Raft, Paxos basics)](./phase-2/05-reliability/03-consensus.md)
- [5.4 Failure Detection & Heartbeats](./phase-2/05-reliability/04-failure-detection.md)
- [5.5 Circuit Breaker Pattern](./phase-2/05-reliability/05-circuit-breaker.md)

#### Week 6: Consistency & Transactions
- [6.1 Strong vs Eventual Consistency](./phase-2/06-consistency/01-consistency-models.md)
- [6.2 Distributed Transactions (2PC, Saga)](./phase-2/06-consistency/02-distributed-transactions.md)
- [6.3 Idempotency — Why It Matters](./phase-2/06-consistency/03-idempotency.md)
- [6.4 Vector Clocks & Versioning](./phase-2/06-consistency/04-vector-clocks.md)
- [6.5 Conflict Resolution Strategies](./phase-2/06-consistency/05-conflict-resolution.md)

#### Week 7: Asynchronous Processing
- [7.1 Message Queues — Kafka vs RabbitMQ vs SQS](./phase-2/07-async/01-message-queues.md)
- [7.2 Event-Driven Architecture](./phase-2/07-async/02-event-driven.md)
- [7.3 Pub/Sub Pattern](./phase-2/07-async/03-pub-sub.md)
- [7.4 Task Queues & Background Jobs](./phase-2/07-async/04-task-queues.md)
- [7.5 Stream Processing Basics](./phase-2/07-async/05-stream-processing.md)

---

### Phase 3: Data Systems Deep Dive

Master the systems that store and process your data.

#### Week 8: Database Internals
- [8.1 How Databases Store Data (B-Trees, LSM Trees)](./phase-3/08-db-internals/01-storage-engines.md)
- [8.2 Query Optimization](./phase-3/08-db-internals/02-query-optimization.md)
- [8.3 Connection Pooling](./phase-3/08-db-internals/03-connection-pooling.md)
- [8.4 Database Locking & Isolation Levels](./phase-3/08-db-internals/04-locking-isolation.md)
- [8.5 Time-Series Databases](./phase-3/08-db-internals/05-time-series-db.md)

#### Week 9: Caching & Search
- [9.1 Redis Deep Dive](./phase-3/09-caching-search/01-redis.md)
- [9.2 Cache Invalidation Strategies](./phase-3/09-caching-search/02-cache-invalidation.md)
- [9.3 Elasticsearch — Full-Text Search](./phase-3/09-caching-search/03-elasticsearch.md)
- [9.4 Distributed Caching](./phase-3/09-caching-search/04-distributed-cache.md)
- [9.5 Cache-Aside vs Read-Through vs Write-Through](./phase-3/09-caching-search/05-caching-patterns.md)

#### Week 10: Big Data Foundations
- [10.1 MapReduce Concept](./phase-3/10-big-data/01-mapreduce.md)
- [10.2 Data Lakes vs Data Warehouses](./phase-3/10-big-data/02-lake-vs-warehouse.md)
- [10.3 Batch vs Real-Time Processing](./phase-3/10-big-data/03-batch-vs-realtime.md)
- [10.4 OLTP vs OLAP](./phase-3/10-big-data/04-oltp-vs-olap.md)
- [10.5 Data Partitioning Strategies](./phase-3/10-big-data/05-partitioning.md)

---

### Phase 4: Real-World System Designs

Apply everything by designing real systems.

#### Week 11-12: Social & Communication Systems
- [11.1 Design Twitter/X](./phase-4/11-social/01-twitter.md)
- [11.2 Design Instagram](./phase-4/11-social/02-instagram.md)
- [11.3 Design Facebook News Feed](./phase-4/11-social/03-newsfeed.md)
- [11.4 Design WhatsApp/Messenger](./phase-4/11-social/04-messenger.md)
- [11.5 Design Notification System](./phase-4/11-social/05-notification.md)

#### Week 13-14: Media & Content Systems
- [12.1 Design YouTube](./phase-4/12-media/01-youtube.md)
- [12.2 Design Netflix](./phase-4/12-media/02-netflix.md)
- [12.3 Design Spotify](./phase-4/12-media/03-spotify.md)
- [12.4 Design Google Drive/Dropbox](./phase-4/12-media/04-file-storage.md)
- [12.5 Design Image Hosting (Imgur)](./phase-4/12-media/05-image-hosting.md)

#### Week 15-16: E-Commerce & Infrastructure
- [13.1 Design Amazon E-Commerce](./phase-4/13-ecommerce/01-amazon.md)
- [13.2 Design Uber/Lyft](./phase-4/13-ecommerce/02-uber.md)
- [13.3 Design Ticketmaster](./phase-4/13-ecommerce/03-ticketmaster.md)
- [13.4 Design URL Shortener (TinyURL)](./phase-4/13-ecommerce/04-url-shortener.md)
- [13.5 Design Rate Limiter](./phase-4/13-ecommerce/05-rate-limiter.md)

---

### Phase 5: Advanced Topics & Interview Prep

Polish your skills and practice under pressure.

#### Week 17: Advanced Patterns
- [14.1 Microservices vs Monolith](./phase-5/14-advanced/01-microservices.md)
- [14.2 Service Mesh](./phase-5/14-advanced/02-service-mesh.md)
- [14.3 CQRS & Event Sourcing](./phase-5/14-advanced/03-cqrs-event-sourcing.md)
- [14.4 Multi-Region Architecture](./phase-5/14-advanced/04-multi-region.md)
- [14.5 Zero Downtime Deployments](./phase-5/14-advanced/05-zero-downtime.md)

#### Week 18: Observability & Operations
- [15.1 Logging at Scale](./phase-5/15-observability/01-logging.md)
- [15.2 Distributed Tracing](./phase-5/15-observability/02-tracing.md)
- [15.3 Metrics & Monitoring](./phase-5/15-observability/03-metrics.md)
- [15.4 Alerting Strategies](./phase-5/15-observability/04-alerting.md)
- [15.5 Chaos Engineering Basics](./phase-5/15-observability/05-chaos-engineering.md)

#### Week 19: Mock Interview Practice
- [16.1 Interview Framework (How to Approach Any Problem)](./phase-5/16-interview/01-framework.md)
- [16.2 Estimation & Back-of-Envelope Calculations](./phase-5/16-interview/02-estimation.md)
- [16.3 Common Mistakes to Avoid](./phase-5/16-interview/03-common-mistakes.md)
- [16.4 Company-Specific Focus Areas](./phase-5/16-interview/04-company-specific.md)
- [16.5 Full Mock Interview Sessions](./phase-5/16-interview/05-mock-sessions.md)

<br>

<br>

---

<br>

## Tech Stack Focus

All examples and code implementations will be in:
- **Java** — Enterprise patterns, Spring ecosystem
- **Go** — High-performance services, cloud-native patterns

<br>

---

<br>

## Recommended Resources

- [System Design Primer](https://github.com/donnemartin/system-design-primer)
- [High Scalability Blog](http://highscalability.com)

<br>

---

<br>


## Tips:

* [cheatsheet](tips/cheatsheet.md)

<br>

---

<br>




## Progress Tracker

```
Phase 1: ⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜ 0/15
Phase 2: ⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜ 0/20
Phase 3: ⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜ 0/15
Phase 4: ⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜ 0/15
Phase 5: ⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜⬜ 0/15

Total: 0/80 topics completed
```


<br>

*Last Updated: 2025-02-03*

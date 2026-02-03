# System Design Cheat Sheet

> Quick reference for numbers, patterns, and concepts used in system design interviews

---

## Numbers You Must Know

### Latency Comparison

| Operation | Time |
|-----------|------|
| L1 cache reference | 0.5 ns |
| L2 cache reference | 7 ns |
| Main memory reference | 100 ns |
| SSD random read | 150 μs |
| Read 1 MB from SSD | 1 ms |
| Disk seek | 10 ms |
| Read 1 MB from disk | 20 ms |
| Send packet CA → Netherlands → CA | 150 ms |

### Data Size Reference

| Unit | Size | Example |
|------|------|---------|
| 1 KB | 1,000 bytes | A short email |
| 1 MB | 1,000 KB | A small image |
| 1 GB | 1,000 MB | A movie |
| 1 TB | 1,000 GB | ~500 hours of video |
| 1 PB | 1,000 TB | ~500 million photos |

### Scale Estimates

| Daily Active Users | Requests/second (rough) |
|-------------------|------------------------|
| 1 million | ~12 req/s |
| 10 million | ~120 req/s |
| 100 million | ~1,200 req/s |
| 1 billion | ~12,000 req/s |

**Formula**: `DAU × (requests per user per day) / 86,400 seconds`

---

## Common Patterns

### Scaling Patterns

```
┌──────────────────────────────────────────────────────────────────┐
│ Problem → Solution Pattern                                       │
├──────────────────────────────────────────────────────────────────┤
│ Single server overloaded     → Horizontal scaling + Load balancer│
│ Database reads slow          → Read replicas + Caching           │
│ Database writes bottleneck   → Sharding / Partitioning           │
│ Large files slow to serve    → CDN + Object storage              │
│ High latency for global users→ Multi-region deployment           │
│ Bursty traffic               → Auto-scaling + Queue              │
│ Single point of failure      → Redundancy + Failover             │
└──────────────────────────────────────────────────────────────────┘
```

### Database Selection Guide

```
┌──────────────────────────────────────────────────────────────────┐
│ Need                          → Consider                         │
├──────────────────────────────────────────────────────────────────┤
│ ACID transactions             → PostgreSQL, MySQL                │
│ High write throughput         → Cassandra, ScyllaDB              │
│ Document storage              → MongoDB, DynamoDB                │
│ Graph relationships           → Neo4j, Amazon Neptune            │
│ Time-series data              → InfluxDB, TimescaleDB            │
│ Full-text search              → Elasticsearch, OpenSearch        │
│ Caching / Sessions            → Redis, Memcached                 │
│ Wide-column / Analytics       → BigTable, HBase                  │
└──────────────────────────────────────────────────────────────────┘
```

### Caching Strategies

```
┌─────────────────────────────────────────────────────────────────┐
│ Strategy           │ When to Use                                │
├────────────────────┼────────────────────────────────────────────│
│ Cache-Aside        │ General purpose, read-heavy workloads      │
│ Read-Through       │ When cache should manage data loading      │
│ Write-Through      │ When consistency is important              │
│ Write-Behind       │ When write performance is critical         │
│ Refresh-Ahead      │ Predictable access patterns                │
└─────────────────────────────────────────────────────────────────┘
```

---

## Back-of-Envelope Calculations

### Storage Calculation Template

```
Given:
- Users: X
- Data per user: Y
- Retention: Z years

Storage = X × Y × 365 × Z
        + Replication factor (usually 3x)
        + Growth buffer (20-30%)
```

### Bandwidth Calculation Template

```
Given:
- Requests per second: R
- Average response size: S

Bandwidth = R × S × 8 (bits per byte)
          = X Gbps
```

### Server Estimation Template

```
Given:
- Peak QPS: Q
- QPS per server: S (typically 1000-10000 for web servers)

Servers needed = Q / S × safety factor (1.5-2x)
```

---

## Common Components

### API Gateway Responsibilities
- Rate limiting
- Authentication/Authorization
- Request routing
- Load balancing
- SSL termination
- Request/Response transformation

### Load Balancer Algorithms
- **Round Robin**: Simple, equal distribution
- **Weighted Round Robin**: Based on server capacity
- **Least Connections**: Route to least busy server
- **IP Hash**: Consistent routing for same client
- **Least Response Time**: Route to fastest server

### Message Queue Use Cases
- Asynchronous processing
- Load leveling (handle traffic spikes)
- Decoupling services
- Reliable delivery (with persistence)
- Fan-out distribution

---

## Interview Framework

### Step 1: Clarify Requirements (2-3 min)
- Functional requirements (what should it do?)
- Non-functional requirements (scale, latency, availability)
- Constraints and assumptions

### Step 2: Estimate Scale (3-5 min)
- Users (DAU, MAU)
- Traffic (QPS, peak QPS)
- Storage (data size, growth rate)
- Bandwidth

### Step 3: High-Level Design (10-15 min)
- Draw main components
- Show data flow
- Identify APIs

### Step 4: Deep Dive (15-20 min)
- Database schema
- Detailed component design
- Handle edge cases

### Step 5: Wrap Up (5 min)
- Identify bottlenecks
- Discuss trade-offs
- Mention future improvements

---

## Common Trade-offs

| Trade-off | Option A | Option B |
|-----------|----------|----------|
| CAP Theorem | Consistency | Availability |
| Latency vs Throughput | Optimize for speed | Optimize for volume |
| SQL vs NoSQL | ACID, complex queries | Scale, flexibility |
| Sync vs Async | Immediate feedback | Better performance |
| Monolith vs Microservices | Simplicity | Scalability |
| Push vs Pull | Real-time updates | Client control |

---
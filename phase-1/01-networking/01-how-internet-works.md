# 1.1 How the Internet Works

> "You can't design distributed systems if you don't understand how they communicate."

## Learning Objectives

By the end of this module, you will understand:
1. What happens when you type a URL and press Enter
2. The OSI model and why it matters for system design
3. How data travels across the internet
4. Key concepts: latency, bandwidth, throughput

---

## The Theory (Know-How)

### What Actually Happens When You Visit google.com?

This simple action triggers a complex sequence of events. Understanding this is **foundational** to system design because every distributed system relies on these mechanisms.

```
┌─────────────────────────────────────────────────────────────────────┐
│                    The Journey of a Request                         │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  1. Browser parses URL                                              │
│         ↓                                                           │
│  2. DNS Lookup (Where is google.com?)                               │
│         ↓                                                           │
│  3. TCP Connection (Three-way handshake)                            │
│         ↓                                                           │
│  4. TLS Handshake (If HTTPS)                                        │
│         ↓                                                           │
│  5. HTTP Request Sent                                               │
│         ↓                                                           │
│  6. Server Processes Request                                        │
│         ↓                                                           │
│  7. HTTP Response Received                                          │
│         ↓                                                           │
│  8. Browser Renders Page                                            │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Why This Matters for System Design

Every step above is a potential:
- **Latency source** — Each step takes time
- **Failure point** — Each step can fail
- **Optimization opportunity** — Each step can be improved

---

## The OSI Model (Simplified for Engineers)

The OSI model isn't just textbook knowledge — it helps you **reason about where problems occur**.

```
┌─────────────────────────────────────────────────────────────────────┐
│                    Practical OSI Model                              │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  Layer 7: Application    │ HTTP, WebSocket, gRPC                    │
│                          │ → What protocol should my service use?   │
│  ────────────────────────┼───────────────────────────────────────   │
│  Layer 4: Transport      │ TCP, UDP                                 │
│                          │ → Reliable or fast?                      │
│  ────────────────────────┼───────────────────────────────────────   │
│  Layer 3: Network        │ IP, Routing                              │
│                          │ → How do packets find their way?         │
│  ────────────────────────┼───────────────────────────────────────   │
│  Layer 1-2: Physical/    │ Ethernet, WiFi                           │
│  Data Link               │ → Usually abstracted away for us         │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### System Design Relevance:

| Layer | System Design Decision |
|-------|----------------------|
| L7 (Application) | REST vs gRPC vs GraphQL? |
| L4 (Transport) | TCP for reliability or UDP for speed? |
| L3 (Network) | How to route traffic across regions? |
| L4 Load Balancer | Cheaper, faster, but limited visibility |
| L7 Load Balancer | Can inspect HTTP headers, route by path |

---

## Critical Metrics: Latency, Bandwidth, Throughput

### Latency — The Time Factor

**Definition**: Time it takes for data to travel from source to destination.

```
┌─────────────────────────────────────────────────────────────────────┐
│                    Latency Numbers Every Engineer Should Know       │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  L1 cache reference                           0.5 ns                │
│  L2 cache reference                           7 ns                  │
│  Main memory reference                        100 ns                │
│  SSD random read                              150,000 ns (150 μs)   │
│  Read 1 MB sequentially from SSD              1,000,000 ns (1 ms)   │
│  Round trip within same datacenter            500,000 ns (0.5 ms)   │
│  Round trip US East → West                    40,000,000 ns (40 ms) │
│  Round trip US → Europe                       80,000,000 ns (80 ms) │
│  Round trip US → Australia                    200,000,000 ns (200ms)│
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

**Why This Matters**: 
- A user in Australia accessing a US server adds 200ms latency **per request**
- This is why CDNs and multi-region deployments exist

### Bandwidth vs Throughput

```
Bandwidth = Maximum capacity of the pipe
Throughput = Actual data transferred

Think of it as:
┌──────────────────────────────────────────────────────┐
│  Highway Analogy                                     │
│  ─────────────────                                   │
│  Bandwidth  = Number of lanes (potential capacity)   │
│  Throughput = Actual cars passing per hour           │
│  Latency    = Time for one car to cross              │
└──────────────────────────────────────────────────────┘
```

---

## Deep Dive: The TCP Three-Way Handshake

This is **why establishing connections takes time** and why connection pooling matters.

```
┌───────────────────────────────────────────────────────────────────┐
│                    TCP Three-Way Handshake                        │
├───────────────────────────────────────────────────────────────────┤
│                                                                   │
│     Client                              Server                    │
│        │                                   │                      │
│        │──────── SYN (seq=x) ─────────────→│  "Hey, want to talk?"│
│        │                                   │                      │
│        │←─────── SYN-ACK (seq=y, ack=x+1) ─│  "Sure, I'm ready"   │
│        │                                   │                      │
│        │──────── ACK (ack=y+1) ───────────→│  "Great, let's go"   │
│        │                                   │                      │
│        │         Connection Established    │                      │
│                                                                   │
│  Time cost: 1.5 × Round Trip Time (RTT)                           │
│                                                                   │
└───────────────────────────────────────────────────────────────────┘
```

### System Design Implication

If RTT to your server is 40ms, **every new connection costs 60ms just for the handshake**.

**Solutions we'll explore later**:
- Connection pooling (reuse connections)
- HTTP/2 multiplexing (multiple requests, one connection)
- Keep-alive connections

---

## Code Example: Measuring Latency

### Go: Simple HTTP Client with Timing

```go
package main

import (
    "fmt"
    "io"
    "net/http"
    "net/http/httptrace"
    "time"
)

func main() {
    url := "https://www.google.com"
    
    // Create a trace to measure each phase
    var dnsStart, dnsDone, connectStart, connectDone, tlsStart, tlsDone time.Time
    var firstByte time.Time
    
    trace := &httptrace.ClientTrace{
        DNSStart:          func(_ httptrace.DNSStartInfo) { dnsStart = time.Now() },
        DNSDone:           func(_ httptrace.DNSDoneInfo) { dnsDone = time.Now() },
        ConnectStart:      func(_, _ string) { connectStart = time.Now() },
        ConnectDone:       func(_, _ string, _ error) { connectDone = time.Now() },
        TLSHandshakeStart: func() { tlsStart = time.Now() },
        TLSHandshakeDone:  func(_ tls.ConnectionState, _ error) { tlsDone = time.Now() },
        GotFirstResponseByte: func() { firstByte = time.Now() },
    }
    
    req, _ := http.NewRequest("GET", url, nil)
    req = req.WithContext(httptrace.WithClientTrace(req.Context(), trace))
    
    start := time.Now()
    resp, err := http.DefaultClient.Do(req)
    if err != nil {
        panic(err)
    }
    defer resp.Body.Close()
    io.ReadAll(resp.Body)
    total := time.Since(start)
    
    fmt.Printf("DNS Lookup:    %v\n", dnsDone.Sub(dnsStart))
    fmt.Printf("TCP Connect:   %v\n", connectDone.Sub(connectStart))
    fmt.Printf("TLS Handshake: %v\n", tlsDone.Sub(tlsStart))
    fmt.Printf("First Byte:    %v\n", firstByte.Sub(start))
    fmt.Printf("Total:         %v\n", total)
}
```

### Java: HttpClient with Timing

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.time.Duration;
import java.time.Instant;

public class LatencyMeasurement {
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newBuilder()
            .connectTimeout(Duration.ofSeconds(10))
            .build();
        
        HttpRequest request = HttpRequest.newBuilder()
            .uri(URI.create("https://www.google.com"))
            .GET()
            .build();
        
        // Measure total request time
        Instant start = Instant.now();
        HttpResponse<String> response = client.send(request, 
            HttpResponse.BodyHandlers.ofString());
        Instant end = Instant.now();
        
        Duration latency = Duration.between(start, end);
        
        System.out.println("Status: " + response.statusCode());
        System.out.println("Latency: " + latency.toMillis() + " ms");
        
        // Why this matters:
        // If this is 200ms for one request, and your page makes 50 requests,
        // that's 10 seconds of latency (without parallelization)!
    }
}
```

---

## Key Takeaways for System Design Interviews

### 1. "Where is the latency coming from?"

When designing systems, always ask:
- Network latency (geographic distance)
- DNS resolution time
- Connection establishment (TCP + TLS)
- Server processing time
- Data transfer time

### 2. The Numbers Game

Memorize approximate latencies:
- Same datacenter: ~0.5ms
- Same region: ~1-5ms  
- Cross-region (US): ~40ms
- Cross-continent: ~80-200ms

### 3. Design Implications

| Problem | Solution Pattern |
|---------|-----------------|
| High latency to users | CDN, edge servers, multi-region |
| Connection overhead | Connection pooling, HTTP/2 |
| DNS resolution slow | DNS caching, multiple DNS providers |
| Data transfer slow | Compression, pagination, caching |

---

## Self-Check Questions

Before moving on, make sure you can answer:

1. **What are the main steps when a browser loads a webpage?**
2. **Why does a TCP connection require 1.5 RTT to establish?**
3. **If your server is in US-East and a user is in Tokyo, what's the minimum latency you can expect?**
4. **What's the difference between L4 and L7 load balancers?**
5. **Why might you choose UDP over TCP for a video streaming service?**

---

## Further Reading

- [High Performance Browser Networking](https://hpbn.co/) (Free online book)
- [Google's Latency Numbers](https://gist.github.com/jboner/2841832)

---

## Next: [1.2 HTTP/HTTPS Deep Dive](./02-http-https.md)

---

*Progress: 1/80 topics*
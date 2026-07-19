
## 20. Horizontal Scaling (Scale Out)

**Horizontal scaling** means increasing system capacity by **adding more servers** instead of upgrading a single server.

```text
Clients
    |
Load Balancer
   / | \
 S1 S2 S3 ... Sn
```

Incoming requests are distributed across multiple servers, allowing the system to handle more traffic.

### Advantages

- Easily handles increasing traffic
- High availability (one server can fail without stopping the system)
- No fixed limit on scaling
- Cost-effective using commodity servers

### Trade-offs

- More complex to design and manage
- Requires **stateless servers**
- Needs a **load balancer**
- Database also needs to scale (Replication/Sharding)

> Horizontal scaling is the preferred approach for large-scale systems like Google, Amazon, and Netflix.

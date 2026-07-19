## 21. Load Balancers

A **Load Balancer** distributes incoming requests across multiple servers to prevent any single server from becoming overloaded.

```text
Clients
    |
Load Balancer
   / | \
 S1 S2 S3
```

It acts as the **traffic manager**, sending requests to healthy and available servers.

### Common Algorithms

- **Round Robin** – Sends requests to servers one by one.
- **Least Connections** – Sends requests to the server with the fewest active connections.
- **Weighted** – Servers with higher capacity receive more traffic.

### Health Checks

The load balancer continuously checks server health.

If a server goes down, traffic is automatically redirected to healthy servers.

### Advantages

- Improves scalability
- Increases availability
- Prevents server overload
- Automatically handles server failures

### Trade-offs

- Adds an extra component to manage
- Can become a single point of failure if not made highly available

> Load balancers are typically placed in front of application servers and are essential for horizontally scaled systems.

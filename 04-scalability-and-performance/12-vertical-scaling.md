# Vertical Scaling (Scaling Up)

Vertical scaling is the process of increasing the resources of a **single server** to handle more load.

Instead of adding more servers, we make the existing server more powerful.

```text
        Before

     ┌──────────────┐
     │   4 CPU      │
     │   8 GB RAM   │
     │   500 GB SSD │
     └──────────────┘

              │
      Upgrade Hardware
              │

              ▼

     ┌──────────────┐
     │   32 CPU     │
     │ 128 GB RAM   │
     │   4 TB SSD   │
     └──────────────┘
```

---

# Why Do We Need Vertical Scaling?

As traffic increases, a server may run out of:

- CPU
- Memory
- Disk
- Network bandwidth

Instead of changing the architecture, we simply upgrade the machine.

---

# Example

A startup begins with:

- 2 CPU
- 4 GB RAM

After reaching 1 million users:

- 16 CPU
- 64 GB RAM

The application continues running on a single machine.

---

# Advantages

- Easy to implement
- No application changes
- No distributed system complexity
- Easier debugging
- No data synchronization issues

---

# Disadvantages

- Hardware has physical limits
- Expensive high-end servers
- Single point of failure
- Downtime may be required during upgrades
- Cannot scale indefinitely

---

# Real-World Example

A small e-commerce website starts with a basic PostgreSQL server.

As traffic grows, the company upgrades the server by adding:

- More CPUs
- More RAM
- Faster SSDs

No changes are required in the application.

---

# Vertical Scaling vs Horizontal Scaling

| Vertical Scaling | Horizontal Scaling |
|------------------|--------------------|
| Scale Up | Scale Out |
| Upgrade one server | Add more servers |
| Easier | More complex |
| Limited by hardware | Nearly unlimited scaling |
| Single point of failure | Better fault tolerance |

---

# When Do We Use Vertical Scaling?

Vertical scaling is suitable when:

- The application is small.
- Traffic is manageable.
- Simplicity is preferred.
- Distributed systems are unnecessary.

---

# Trade-offs

| Advantages | Disadvantages |
|------------|---------------|
| Simple | Limited scalability |
| Easy maintenance | Expensive hardware |
| No distributed complexity | Single point of failure |
| No routing required | Downtime during upgrades |

---

# Key Takeaways

- Vertical scaling upgrades a **single server**.
- Improves CPU, RAM, and storage.
- Easy to implement.
- Limited by hardware capacity.
- Best suited for small to medium-sized systems.

# Database Replication

Database replication is the process of maintaining **multiple copies of the same database** across different servers (called replicas).

Instead of storing data on only one machine, the same data exists on multiple machines.

```text
            Write
             │
             ▼
      Primary Database
      (Leader / Master)
       /      |      \
      /       |       \
     ▼        ▼        ▼
Replica 1  Replica 2  Replica 3
(Read)     (Read)     (Read)
```

---

# Why do we need replication?

Imagine Instagram has only one database.

```text
Users
   │
   ▼
Database
```

Problems:

- Database crashes → Entire application goes down.
- Millions of users reading simultaneously overload the server.
- No backup if hardware fails.

Replication solves these problems.

---

# Types of Replication

## 1. Primary-Replica (Leader-Follower)

The most common architecture.

```text
               Write
                 │
                 ▼
            Primary DB
            /   |   \
           /    |    \
          ▼     ▼     ▼
      Replica Replica Replica
```

### Writes

All `INSERT`, `UPDATE`, and `DELETE` operations go to the Primary.

```text
User
  │
INSERT
  │
  ▼
Primary
```

---

### Reads

Read requests can go to replicas.

```text
          User
        /  |   \
       ▼   ▼    ▼
Replica Replica Replica
```

This dramatically increases read capacity.

### Example

Suppose:

- Primary handles **10,000 reads/sec**

Without replication:

```text
10,000 Users
      │
      ▼
Primary
```

Maximum throughput = **10k reads/sec**

Now add **3 replicas**.

```text
          Reads
             │
             ▼
          Primary
         /   |   \
        ▼    ▼    ▼
   Replica Replica Replica
```

Now roughly:

```
4 × 10,000

≈ 40,000 reads/sec
```

Same data.

4× more read throughput.

---

# Replication Lag

Replication is **not always instantaneous**.

Example:

```
10:00:00

User changes profile picture

        │
        ▼
Primary Updated

Replica
(still old)
```

After **200 ms**:

```
Replica Updated
```

This delay is called **Replication Lag**.

### Example

Alice changes her username.

Immediately refreshes the page.

Request goes to a replica.

Replica still returns:

```
Alice123
```

instead of:

```
Alice456
```

This is called **stale data**.

---

# Synchronous Replication

The Primary waits until replicas acknowledge the write.

```text
Write

Primary
   │
   ▼
Replica 1 ✓

Replica 2 ✓

Replica 3 ✓

Return Success
```

## Advantages

- Strong consistency
- No stale reads

## Disadvantages

- Slower writes
- Higher latency

---

# Asynchronous Replication

The Primary immediately returns success.

Replication happens later.

```text
Write

Primary
  │
Success

Later

Replica
Replica
Replica
```

## Advantages

- Fast writes
- Lower latency

## Disadvantages

- Replication lag
- Possible stale reads

Most large internet companies use asynchronous replication because performance is usually more important than immediate consistency.

---

# Read Scaling

Instead of every request hitting one server:

```text
1000 Users
     │
     ▼
Primary
```

Use replicas:

```text
1000 Users

 /   |   |   \

▼    ▼   ▼    ▼

Replica
Replica
Replica
Primary
```

Reads become distributed across multiple machines.

---

# High Availability (HA)

Suppose the Primary crashes.

Without replication:

```text
Primary
   ✗

Application Down
```

With replication:

```text
Primary ✗

Replica
Replica

↓

One Replica
becomes Primary
```

Users experience only a brief interruption instead of a complete outage.

This process is called **Failover**.

---

# Automatic Failover

Many databases automatically promote a replica to become the new Primary.

```text
Primary
   ✗

↓

Replica 2

↓

Promoted

↓

New Primary
```

Applications reconnect to the new Primary.

---

# Disaster Recovery

Suppose an entire data center fails.

```text
Mumbai Data Center

Primary ✗
Replica ✗
```

Another region already has a copy.

```text
Singapore Data Center

Replica
Replica
```

Traffic switches there.

Replication across regions protects against regional failures.

---

# Multi-Region Replication

```text
India

Primary

     │

──────────── Internet ────────────

US Replica

Europe Replica

Singapore Replica
```

## Benefits

- Lower latency
- Disaster recovery
- Better availability

---

# Read-After-Write Consistency Problem

User changes password.

Immediately logs in.

If login reads from a replica:

```text
Replica

Old Password
```

Login fails.

## Solutions

- Read from the Primary immediately after writing.
- Use sticky sessions (route a user's reads to the Primary for a short period after a write).
- Wait until replication catches up.

---

# Replication vs Sharding

These concepts are often confused.

| Replication | Sharding |
|-------------|----------|
| Same data copied to multiple servers | Data split across multiple servers |
| Improves read performance | Improves storage and write scalability |
| Provides high availability | Provides horizontal scaling |
| Multiple copies of the same data | Each server stores only part of the data |

## Replication

```text
Primary

Users A-Z

↓

Replica

Users A-Z

↓

Replica

Users A-Z
```

## Sharding

```text
Shard 1

Users A-F

Shard 2

Users G-M

Shard 3

Users N-Z
```

---

# When do we use Replication?

Use replication when you need:

- High read throughput
- High availability
- Fault tolerance
- Disaster recovery
- Backup copies
- Multi-region deployments

---

# Interview Example

**Question:** *Design Instagram.*

A good answer:

> Instagram is a read-heavy application. Posts are written once but viewed millions of times. I would use a Primary-Replica architecture where all writes go to the Primary database while multiple Replicas serve read traffic. This improves read scalability and provides high availability. Since asynchronous replication introduces replication lag, user-specific actions immediately after a write (such as editing a profile or posting a photo) should temporarily read from the Primary to guarantee read-after-write consistency.

---

# Trade-offs

| Advantages | Disadvantages |
|------------|---------------|
| Improves read scalability | Replication lag |
| High availability | Additional infrastructure cost |
| Fault tolerance | Operational complexity |
| Disaster recovery | Eventual consistency (asynchronous replication) |
| Enables failover | Writes are still limited by the Primary |

---

# Key Takeaways

- Replication creates **multiple copies** of the same data.
- Writes typically go to the **Primary**.
- Reads are distributed across **Replicas**.
- Improves **read scalability**, **availability**, and **fault tolerance**.
- Asynchronous replication is faster but can produce **stale reads**.
- Synchronous replication provides stronger consistency but increases write latency.
- Replication is different from **Sharding**—Replication copies data, whereas Sharding splits data.
- Large-scale systems often combine **Replication**, **Caching**, and **Sharding** to achieve scalability and reliability.

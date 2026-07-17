# Database Sharding

Database sharding is a technique used to **horizontally partition** a database by splitting data across multiple independent databases called **shards**.

Instead of storing **all data on one database**, each shard stores **only a portion of the data**.

```text
                Users

                  │

        ┌─────────┴─────────┐

        ▼                   ▼

     Shard 1            Shard 2

    Users A-M          Users N-Z
```

Unlike replication, where every server stores the **same data**, each shard stores a **different subset** of the data.

---

# Why Do We Need Sharding?

Imagine Instagram has **5 billion users**.

A single database eventually runs into limitations:

- Storage becomes full.
- CPU becomes overloaded.
- Memory becomes insufficient.
- Writes become slower.
- Vertical scaling becomes expensive.

Adding more CPU and RAM can only help so much.

Instead, we divide the data across multiple databases.

---

# Without Sharding

```text
              Users

                │

                ▼

         Single Database

       Users 1 - 5 Billion
```

Problems:

- Huge database size
- High write latency
- Expensive hardware
- Single bottleneck

---

# With Sharding

```text
                 Users

                   │

      ┌────────────┼────────────┐

      ▼            ▼            ▼

   Shard 1      Shard 2      Shard 3

 Users 1-1B   Users 1B-3B   Users 3B-5B
```

Each shard handles only a fraction of the total data.

This distributes:

- Storage
- CPU
- Memory
- Network traffic
- Write operations

---

# How Does Sharding Work?

A **Shard Key** determines which shard stores a piece of data.

Example:

```
User ID = 45821
```

Routing logic determines:

```
45821 → Shard 3
```

The application (or a routing layer) sends the request directly to the correct shard.

---

# Common Sharding Strategies

## 1. Range-Based Sharding

Data is divided into ranges.

Example:

```text
Shard 1

User ID

1 - 1,000,000

----------------------

Shard 2

1,000,001 - 2,000,000

----------------------

Shard 3

2,000,001+
```

### Advantages

- Simple
- Easy to understand
- Efficient for range queries

### Disadvantages

- Uneven data distribution
- Hotspots if newer users are concentrated in one range

---

## 2. Hash-Based Sharding

A hash function determines the shard.

Example:

```
Shard = Hash(UserID) % NumberOfShards
```

Example:

```
User ID = 25

25 % 4 = 1

→ Shard 1
```

### Advantages

- Even distribution
- Prevents hotspots

### Disadvantages

- Difficult to rebalance
- Range queries become expensive

---

## 3. Geographic Sharding

Users are partitioned by location.

```text
India

↓

India Database

----------------

USA

↓

USA Database

----------------

Europe

↓

Europe Database
```

### Advantages

- Lower latency
- Better compliance
- Easier regional scaling

### Disadvantages

- Cross-region queries become complex

---

# Read and Write Flow

Suppose User 12345 logs in.

```
Application

↓

Shard Router

↓

Hash(UserID)

↓

Shard 2

↓

Return Data
```

The application communicates only with the correct shard.

---

# Benefits of Sharding

- Horizontal scalability
- Supports massive datasets
- Higher write throughput
- Reduced storage per database
- Lower latency
- Better resource utilization

---

# Challenges of Sharding

## 1. Cross-Shard Joins

Suppose:

Users are stored in Shard 1.

Orders are stored in Shard 2.

A JOIN now requires querying multiple databases.

Much slower than querying a single database.

---

## 2. Transactions

Transactions across shards become difficult.

Example:

Transfer money between:

```
Account A

Shard 1

↓

Account B

Shard 4
```

Maintaining ACID guarantees is much harder.

---

## 3. Rebalancing

Suppose:

```text
Shard 1

95%

Full

----------------

Shard 2

20%

Used
```

Data needs to be moved.

Migrating data while keeping the system online is difficult.

---

## 4. Operational Complexity

Sharding introduces:

- Routing logic
- Monitoring
- Backup per shard
- Recovery
- Data migration

Managing many databases is significantly harder than managing one.

---

# Sharding vs Partitioning

These terms are often confused.

## Partitioning

A single database is divided internally into partitions.

```text
Database

│

├── Partition A

├── Partition B

└── Partition C
```

Still one database server.

---

## Sharding

Data is distributed across **multiple database servers**.

```text
Shard 1

(Server A)

-------------

Shard 2

(Server B)

-------------

Shard 3

(Server C)
```

Each shard is an independent database.

---

# Sharding vs Replication

| Sharding | Replication |
|----------|-------------|
| Splits data | Copies data |
| Improves write scalability | Improves read scalability |
| Each shard stores unique data | Every replica stores the same data |
| Horizontal scaling | High availability |
| Increases storage capacity | Increases fault tolerance |

---

# Combining Sharding and Replication

Large systems use **both**.

```text
                 Users

                    │

          Shard Router

      ┌────────┴────────┐

      ▼                 ▼

   Shard 1           Shard 2

      │                  │

  ┌───┴───┐          ┌────┴────┐

Replica Replica   Replica Replica
```

Each shard has its own replicas.

Benefits:

- Sharding improves write scalability.
- Replication improves read scalability.
- High availability.
- Fault tolerance.

This is how many large-scale systems are designed.

---

# Real-World Examples

## Instagram

- Users are distributed across shards using User ID.
- Each shard has multiple replicas.
- Images are stored separately in object storage (e.g., Amazon S3).

---

## Amazon

- Customer data is sharded.
- Orders are partitioned.
- Replication ensures high availability.

---

## Facebook

- User profiles are sharded.
- Each shard has several replicas.
- Friend relationships are distributed across multiple databases.

---

# Interview Example

**Question:** *Design a system for 2 billion users.*

A good answer:

> A single database cannot efficiently handle billions of users. I would horizontally shard the database using User ID as the shard key to distribute data across multiple database servers. To improve read performance and fault tolerance, each shard would have one Primary and multiple Replicas. This architecture enables horizontal scaling, high availability, and efficient handling of both read and write traffic.

---

# Trade-offs

| Advantages | Disadvantages |
|------------|---------------|
| Horizontal scalability | Cross-shard joins |
| Better write throughput | Complex transactions |
| Larger storage capacity | Rebalancing challenges |
| Lower latency | Operational complexity |
| Reduced load per server | Choosing the right shard key is critical |

---

# Key Takeaways

- Sharding **splits** data across multiple databases.
- Each shard stores **only a subset** of the data.
- A **Shard Key** determines where data is stored.
- Sharding improves **write scalability** and **storage capacity**.
- Replication and sharding solve different problems and are commonly used together in large-scale systems.
- Choosing the right shard key is one of the most important design decisions because it determines data distribution, scalability, and query performance.

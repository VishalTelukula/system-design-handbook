# Group 5: Distributed Systems

As applications grow, a single server is often no longer enough to handle the increasing number of users and requests. To improve **scalability**, **availability**, and **fault tolerance**, systems are distributed across multiple servers, databases, and even different geographic regions.

A **Distributed System** is a collection of independent computers that work together and appear to users as a single system.

Examples include:

- Google Search
- Netflix
- Amazon
- Facebook
- WhatsApp

Although distributed systems provide many benefits, they also introduce new challenges because multiple machines must communicate over a network.

## Why Use Distributed Systems?

- Handle millions of users simultaneously
- Scale horizontally by adding more servers
- Continue operating even if some machines fail
- Reduce latency by serving users from nearby regions
- Improve reliability and availability

## Challenges in Distributed Systems

Unlike a single computer, distributed systems must deal with problems such as:

- Network failures
- Server crashes
- Data replication
- Data consistency
- Clock synchronization
- Load balancing
- Network latency
- Partial failures (one service fails while others continue)

Because of these challenges, designing distributed systems is much harder than designing applications that run on a single machine.

---

# 24. CAP Theorem

The **CAP Theorem**, proposed by computer scientist **Eric Brewer**, states that a distributed system **cannot simultaneously guarantee all three of the following properties**:

- **Consistency (C)**
- **Availability (A)**
- **Partition Tolerance (P)**

```text
             CAP Theorem

          Consistency (C)
      Every read gets latest data
               /\
              /  \
             /    \
            /      \
Availability ------ Partition Tolerance
 Every request      System continues
 gets a response    despite network failures
```

Since **network partitions are unavoidable** in distributed systems, the real trade-off is usually between **Consistency** and **Availability**.

---

## 1. Consistency (C)

Every client always reads the **most recent data**.

Once data is written successfully, every future read should return that updated value.

### Example

Suppose your bank account balance is updated from ₹5000 to ₹3000.

```
Write:
Balance = ₹3000
```

Every user, regardless of which server they connect to, should immediately see:

```
₹3000
```

No server should return the old balance.

### Suitable For

- Banking systems
- Inventory management
- Airline booking
- Financial transactions

---

## 2. Availability (A)

Every request receives a response, even if some servers are unavailable.

The response may not always contain the latest data, but the system never becomes unavailable.

### Example

Suppose you post a photo on social media.

One server still has the old data.

A friend may not see your latest post immediately, but the application continues working.

This is acceptable for many social applications.

### Suitable For

- Social media
- Product catalogs
- Recommendation systems
- Analytics dashboards

---

## 3. Partition Tolerance (P)

A distributed system continues functioning even when communication between servers fails.

### Example

Imagine two data centers:

```text
Data Center A  ❌ Network Failure ❌  Data Center B
```

Even though they cannot communicate, users should still be able to use the application.

Network failures are inevitable in distributed systems, so **Partition Tolerance is considered mandatory**.

---

# Why Can't We Have All Three?

Imagine two servers storing the same data.

```text
Server A             Server B
Balance = ₹5000      Balance = ₹5000
```

A user updates Server A:

```text
Balance = ₹3000
```

Immediately afterward, the network connection between A and B fails.

```text
Server A   ❌ Network Partition ❌   Server B
```

Now another user requests the balance from Server B.

The system has two choices:

### Option 1: Return Old Data

Server B responds with:

```
₹5000
```

✔ Available

❌ Not Consistent

This is an **AP System**.

---

### Option 2: Refuse the Request

Server B says:

```
Unable to process request.
```

✔ Consistent

❌ Not Available

This is a **CP System**.

Because of the network partition, it is impossible to have both perfect consistency and perfect availability.

---

# CP Systems (Consistency + Partition Tolerance)

A **CP system** prioritizes correct and up-to-date data.

If the latest data cannot be guaranteed, it may reject the request.

```text
Write Data
     |
Replication Failed
     |
Reject Reads
```

### Advantages

- Always returns the latest data
- Prevents stale reads
- Suitable for critical applications

### Trade-offs

- Requests may fail during network partitions
- Lower availability

### Examples

- MongoDB (depending on configuration)
- HBase
- ZooKeeper
- etcd

### Best For

- Banking
- Payments
- Inventory
- Ticket booking

---

# AP Systems (Availability + Partition Tolerance)

An **AP system** always responds, even if some data is temporarily outdated.

Different servers eventually synchronize.

```text
Write Data
     |
Network Partition
     |
Return Existing Data
     |
Synchronize Later
```

This concept is called **Eventual Consistency**.

### Advantages

- High availability
- Better user experience
- Handles network failures gracefully

### Trade-offs

- Users may temporarily see stale data
- Data becomes consistent later

### Examples

- Cassandra
- Amazon DynamoDB
- CouchDB
- Riak

### Best For

- Social media
- News feeds
- Product catalogs
- Analytics

---

# CP vs AP

| CP | AP |
|----|----|
| Prioritizes Consistency | Prioritizes Availability |
| May reject requests | Always responds |
| Latest data guaranteed | Data may be temporarily stale |
| Better for financial systems | Better for social applications |

---

# Real-World Examples

### Banking

You transfer ₹10,000.

Would you rather:

- See the correct balance after waiting a second? ✅
- Or instantly see the wrong balance? ❌

Banking chooses **CP**.

---

### Instagram

You upload a photo.

Some users may not see it for a few seconds.

This delay is acceptable because the app remains available.

Instagram chooses **AP** for many features.

---

# Key Takeaways

- Distributed systems consist of multiple machines working together.
- Network failures are unavoidable.
- CAP Theorem states that during a network partition, you must choose between **Consistency** and **Availability**.
- **CP systems** prioritize correct data.
- **AP systems** prioritize uninterrupted service.
- The right choice depends on the application's business requirements.

> Understanding CAP Theorem helps you choose the right architecture when designing scalable and fault-tolerant distributed systems.

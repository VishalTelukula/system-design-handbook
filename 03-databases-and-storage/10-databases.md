# Databases

A database is an organized collection of data that supports efficient storage, retrieval, and manipulation. But there is no single **"best"** database. Different data shapes and access patterns call for different types.

| Application | Database Type | Examples |
|-------------|--------------|----------|
| Relational | SQL | PostgreSQL, MySQL |
| Document | NoSQL | MongoDB |
| Key-Value | NoSQL | Redis, DynamoDB |
| Graph | Graph DB | Neo4j |

## Types of Databases

### Relational Databases (PostgreSQL, MySQL)

Store data in structured tables with defined relationships.

**Best for**
- Transactional systems
- Strong consistency
- Structured data

---

### Document Databases (MongoDB)

Store data as flexible JSON-like documents.

**Best for**
- Evolving schemas
- Semi-structured data

---

### Key-Value Stores (Redis, DynamoDB)

Store data as key-value pairs for extremely fast lookups.

**Best for**
- Caching
- Sessions
- Simple lookups

---

### Graph Databases (Neo4j)

Store relationships as first-class citizens.

**Best for**
- Social networks
- Recommendation systems
- Fraud detection

---

## Choosing a Database

Choose a database based on:

- Data model
- Query patterns
- Scalability requirements

There is no single correct database for every use case.

The most common design decision is choosing between SQL and NoSQL.

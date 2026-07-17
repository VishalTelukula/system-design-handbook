
# SQL vs NoSQL

SQL databases enforce a strict schema and support ACID transactions.

NoSQL databases trade some of that rigidity for flexibility and horizontal scalability.

| SQL Databases | NoSQL Databases |
|--------------|-----------------|
| Structured schema | Flexible schema |
| ACID transactions | Eventual consistency |
| Complex joins | No joins needed |
| Vertical scaling | Horizontal scaling |

## Choose SQL When

- Strong consistency is required
- Banking systems
- Inventory systems
- Complex joins
- Well-defined schemas
- ACID guarantees

---

## Choose NoSQL When

- Horizontal scalability
- Frequently changing schema
- High write throughput
- Unstructured data
- Logs
- Social media posts

---

## Real World

Most production systems use both.

Example:

- Orders → PostgreSQL
- Product Catalog → MongoDB

The important interview point is explaining **why** one database was chosen for a specific use case.

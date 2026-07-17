# Denormalization

Normalization avoids duplicate data by splitting information across multiple tables.

Denormalization intentionally stores duplicate data to reduce joins.

## Normalized

### Orders

| order_id | user_id | product_id |
|----------|---------|------------|

### Users

| user_id | name |
|---------|------|

### Products

| product_id | title | price |
|------------|-------|-------|

Requires multiple JOINs.

---

## Denormalized

### Orders

| order_id | user_id | user_name | product_id | product_title | price |
|----------|---------|-----------|------------|---------------|-------|

A single query returns all required data.

## Trade-off

Pros

- Faster reads
- Fewer joins

Cons

- Duplicate data
- Harder updates
- Data consistency challenges

Denormalization is a read optimization and is common in NoSQL databases.

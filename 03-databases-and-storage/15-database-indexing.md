
# Database Indexing

Without an index, the database scans every row to find matching data.

For large datasets, this becomes extremely slow.

An index works like the index at the back of a textbook.

Most databases use **B-Tree indexes**.

A B-Tree provides approximately **O(log n)** lookups.

When you create an index on a column (for example, `email`), the database builds a B-Tree mapping values to row locations.

## Advantages

- Faster reads
- Faster searches
- Improves WHERE clause performance
- Improves JOIN performance

## Disadvantages

- Slower INSERT
- Slower UPDATE
- Additional storage

## Good Columns to Index

- WHERE columns
- JOIN columns

Avoid indexing every column.

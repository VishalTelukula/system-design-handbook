# Vertical Partitioning

Vertical partitioning splits a wide table into multiple narrower tables.

Each partition contains related columns and shares the same primary key.

## Example

### Users Table

| id | name | email | password_hash | avatar | bio | billing_address | card_number | login_count |
|----|------|-------|---------------|--------|-----|-----------------|-------------|-------------|

↓

### Profile Table

| id | name | email | avatar | bio |
|----|------|-------|--------|-----|

### Auth Table

| id | password_hash | login_count |
|----|---------------|-------------|

### Billing Table

| id | billing_address | card_number |
|----|-----------------|-------------|

## Benefits

- Reads fewer columns
- Faster queries
- Better security
- Independent indexing
- Independent optimization

Vertical partitioning separates data based on access patterns.

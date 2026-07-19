

## Idempotency

**Idempotency** ensures that performing the **same request multiple times produces the same result**, preventing duplicate operations.

This is important in distributed systems where a request may fail or time out, causing the client to retry.

### Example

A customer makes a payment of **$50**.

```text
Client
   |
POST /payments
Idempotency-Key: abc-123
   |
Server processes payment
   |
Network timeout ❌
```

The client doesn't know if the payment succeeded, so it retries:

```text
POST /payments
Idempotency-Key: abc-123
```

The server recognizes the same **Idempotency-Key** and returns the previous result instead of processing the payment again.

```text
First Request
      |
Process Payment
      |
Store Idempotency Key
      |
Retry with Same Key
      |
Return Previous Response
```

### Why It Matters

Without idempotency:

- Customer may be charged twice
- Duplicate orders may be created
- Multiple emails or notifications may be sent

With idempotency:

- Duplicate requests are safely ignored
- Only one operation is performed
- Client receives the same response every time

### Common Use Cases

- Payment processing
- Order creation
- Ticket booking
- Money transfers
- API retries

### HTTP Methods

| Method | Idempotent? |
|---------|-------------|
| `GET` | ✅ Yes |
| `PUT` | ✅ Yes |
| `DELETE` | ✅ Yes |
| `POST` | ❌ No (unless an Idempotency Key is used) |

### Interview Tip

Whenever you discuss **payments**, **orders**, or any operation where duplicates are harmful, mention **Idempotency** to ensure the same request is processed only once.

> Idempotency is essential for building reliable distributed systems that can safely handle retries.

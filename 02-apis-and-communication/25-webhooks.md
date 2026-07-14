## 11. Webhooks

**Webhooks** allow one application to automatically notify another application when a specific event occurs.

Instead of the client repeatedly asking:

```text
"Has anything changed?"
"Has anything changed?"
"Has anything changed?"
```

the server sends a notification **only when something happens**.

This is often called an **event-driven** approach.

### How Webhooks Work

First, your application provides a **callback URL** to another service.

```text
Your App
   |
   | Register webhook URL
   | https://myapp.com/webhook
   v
External Service
```

Later, when an event occurs, the external service sends an HTTP request to that URL.

```text
External Service                 Your App
       |                            |
       |--- POST /webhook -------->|
       |    payment.completed      |
       |                            |
       |<------- 200 OK ------------|
```

### Example: Payment Notification

Suppose a user makes a payment through Stripe.

When the payment succeeds, Stripe can send:

```http
POST /webhook
```

```json
{
  "event": "payment.completed",
  "amount": 99.99
}
```

Your application receives the event and can:

* Mark the order as paid
* Send a confirmation email
* Start order processing

### Polling vs Webhooks

| Polling                              | Webhooks                                  |
| ------------------------------------ | ----------------------------------------- |
| Client repeatedly checks for updates | Server sends updates when an event occurs |
| Creates unnecessary requests         | Requests happen only when needed          |
| Can have delays                      | Near real-time notification               |
| Client pulls data                    | Server pushes event notifications         |

### Common Use Cases

Webhooks are widely used for integrations such as:

* **Payment notifications** — payment completed or failed
* **GitHub events** — code pushed or pull request created
* **CI/CD pipelines** — trigger a build after a code push
* **Message delivery** — message delivered or failed
* **Order updates** — order shipped or delivered

### Reliability Challenges

What happens if your application is down when the webhook is sent?

Good webhook systems usually include:

* **Retries** — resend the event if delivery fails
* **Event logging** — store webhook delivery attempts
* **Idempotency** — safely handle the same event more than once
* **Authentication/signature verification** — verify that the webhook came from a trusted source

### WebSockets vs Webhooks

| WebSockets                                     | Webhooks                                  |
| ---------------------------------------------- | ----------------------------------------- |
| Persistent connection                          | Normal HTTP request                       |
| Bidirectional communication                    | Usually one-way notification              |
| Best for real-time client-server communication | Best for service-to-service events        |
| Connection stays open                          | Request is sent only when an event occurs |

### When to Use Webhooks

Use webhooks for **asynchronous event notifications**, especially when integrating with external services.

```text
Event Occurs
     ↓
External Service
     ↓
POST Webhook
     ↓
Your Application
     ↓
Process Event
```

> We have covered how data moves between applications. But where does all that data actually live?

This leads us to **Databases**.

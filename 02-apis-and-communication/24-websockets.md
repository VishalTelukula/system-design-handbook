## 10. WebSockets

**WebSockets** enable **real-time, bidirectional communication** between a client and a server.

In normal HTTP communication, the **client must always initiate the request**.

```text
Client  ---> Request  ---> Server
Client  <--- Response <--- Server
```

But applications such as:

* Chat applications
* Live sports scores
* Multiplayer games
* Collaborative editors
* Real-time notifications
* Typing indicators

need the **server to push updates to the client instantly**.

This is where WebSockets are useful.

### How WebSockets Work

A WebSocket connection starts as a normal HTTP request.

```text
Client                         Server
   |                              |
   |---- HTTP Upgrade Request --->|
   |                              |
   |<--- 101 Switching Protocols -|
   |                              |
   |==== WebSocket Connection ====|
   |                              |
   |------ Send Message --------->|
   |<----- New Message -----------|
   |<----- Live Update -----------|
   |------ Typing Indicator ----->|
```

After the connection is established, it **stays open** until either the client or server closes it.

Both sides can send messages at any time.

### HTTP vs WebSockets

| HTTP                                     | WebSockets                          |
| ---------------------------------------- | ----------------------------------- |
| Client initiates requests                | Client and server can send messages |
| Request-response model                   | Bidirectional communication         |
| Connection usually closes after response | Connection stays open               |
| Good for normal APIs                     | Good for real-time applications     |

### Example: Chat Application

With normal HTTP, the client may need to repeatedly ask:

```text
"Are there any new messages?"
"Are there any new messages?"
"Are there any new messages?"
```

With WebSockets, the server can immediately push a new message:

```text
User A sends message
        ↓
Server receives message
        ↓
Server pushes message to User B instantly
```

### Advantages

* Real-time communication
* Low latency
* Bidirectional communication
* No need for repeated HTTP polling
* Efficient for frequent updates

### Trade-offs

WebSocket connections are **stateful** because the server must keep track of every active connection.

This makes scaling more difficult.

For example:

```text
User 1 ──┐
User 2 ──┼──> Server A
User 3 ──┘

User 4 ──┐
User 5 ──┼──> Server B
User 6 ──┘
```

If **Server A goes down**, all WebSocket connections connected to it are lost and the clients must reconnect.

### When to Use WebSockets

Use WebSockets when your application requires frequent, real-time communication, such as:

* Chat applications
* Live notifications
* Live sports scores
* Multiplayer games
* Collaborative editing
* Real-time dashboards

> WebSockets allow real-time communication between a client and a server. But what if one server needs to automatically notify another server when an event occurs?

For example:

* A payment provider needs to notify your application when a payment succeeds.
* GitHub needs to trigger a CI/CD pipeline when code is pushed.

This is where **Webhooks** come in.

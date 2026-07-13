# 01. Client-Server Architecture

> **Client-Server Architecture** is a computing model in which a **client sends requests** for data or services, and a **server processes those requests and sends back responses**.

---

## What is Client-Server Architecture?

Almost every web application we use is based on a fundamental concept called **Client-Server Architecture**.

It consists of two main components:

### Client

The **client** is the application or device that initiates a request.

Examples:

- Web browser
- Mobile application
- Desktop application
- Frontend web application

For example, when you open a website in your browser, the **browser acts as the client**.

### Server

The **server** is a machine or software process that listens for incoming requests, processes them, and sends responses back to clients.

A server may:

- Retrieve data
- Store data
- Update data
- Delete data
- Perform business logic
- Authenticate users
- Communicate with databases or other services

---

## Basic Request-Response Flow

The basic communication looks like this:

```text
┌──────────────┐                       ┌──────────────┐
│              │       Request         │              │
│    Client    │ ────────────────────► │    Server    │
│              │                       │              │
│   Browser    │ ◄──────────────────── │ Application  │
│  Mobile App  │       Response        │    Server    │
│              │                       │              │
└──────────────┘                       └──────────────┘
```

The process is:

1. The **client sends a request**.
2. The **server receives the request**.
3. The server **processes the request**.
4. The server may interact with a **database, cache, or another service**.
5. The server sends a **response** back to the client.
6. The client displays or uses the received data.

---

## Simple Example

Suppose you open an e-commerce application and search for a laptop.

### Step 1: Client sends a request

```http
GET /products/laptops
```

The browser or mobile application sends a request to the server.

### Step 2: Server processes the request

The server receives the request and may query a database:

```text
Find all products where category = "laptop"
```

### Step 3: Server sends a response

The server may return:

```json
{
  "products": [
    {
      "id": 1,
      "name": "Laptop A",
      "price": 70000
    },
    {
      "id": 2,
      "name": "Laptop B",
      "price": 90000
    }
  ]
}
```

### Step 4: Client displays the result

The browser or mobile application receives the data and displays the products to the user.

---

## A More Realistic Architecture

In real-world applications, the server usually communicates with other components.

```text
┌────────────┐
│   Client   │
│  Browser   │
└─────┬──────┘
      │
      │ Request
      ▼
┌────────────┐
│   Server   │
│  Backend   │
└─────┬──────┘
      │
      │ Query
      ▼
┌────────────┐
│  Database  │
└─────┬──────┘
      │
      │ Data
      ▼
┌────────────┐
│   Server   │
└─────┬──────┘
      │
      │ Response
      ▼
┌────────────┐
│   Client   │
└────────────┘
```

The flow becomes:

```text
Client → Server → Database
Client ← Server ← Database
```

For example:

```text
Browser
   │
   │ GET /users/123
   ▼
Backend Server
   │
   │ SELECT * FROM users WHERE id = 123
   ▼
Database
   │
   │ User Data
   ▼
Backend Server
   │
   │ JSON Response
   ▼
Browser
```

---

## What Can a Client Request?

A client commonly requests the server to perform **CRUD operations**.

| Operation | Meaning | HTTP Method |
|---|---|---|
| Create | Add new data | `POST` |
| Read | Retrieve data | `GET` |
| Update | Replace or partially modify data | `PUT` / `PATCH` |
| Delete | Remove data | `DELETE` |

### Example

```text
GET /users/1
```

Retrieve a user.

```text
POST /users
```

Create a new user.

```text
PATCH /users/1
```

Partially update a user.

```text
DELETE /users/1
```

Delete a user.

---

## How Does the Client Find the Server?

This leads to an important question:

> **How does the client know where the server is located?**

Every server connected to a network has an **IP address**.

For example:

```text
142.250.183.14
```

A client can communicate with a server using its IP address.

However, humans do not want to remember numerical IP addresses.

Instead, we use domain names:

```text
example.com
```

The **Domain Name System (DNS)** translates the domain name into an IP address.

```text
example.com
     │
     ▼
    DNS
     │
     ▼
93.184.216.34
     │
     ▼
   Server
```

The simplified flow is:

```text
User enters a domain name
        ↓
DNS finds the server's IP address
        ↓
Client connects to the server
        ↓
Client sends an HTTP/HTTPS request
        ↓
Server processes the request
        ↓
Server sends a response
```

This connects Client-Server Architecture to the next important concepts:

- IP Addresses
- DNS
- HTTP / HTTPS

---

## One Server Can Serve Many Clients

A server is not limited to communicating with one client.

Many clients can send requests to the same server.

```text
┌──────────┐
│ Client A │ ───────┐
└──────────┘        │
                    │
┌──────────┐        │        ┌────────────┐
│ Client B │ ───────┼──────► │   Server   │
└──────────┘        │        └────────────┘
                    │
┌──────────┐        │
│ Client C │ ───────┘
└──────────┘
```

For example, thousands or millions of users may access the same application.

As the number of clients increases, a single server may no longer be enough.

This eventually introduces concepts such as:

- Vertical Scaling
- Horizontal Scaling
- Load Balancing
- Caching
- CDNs

---

## Client vs Server

| Client | Server |
|---|---|
| Initiates requests | Receives requests |
| Usually interacts with the user | Usually runs in the background |
| Requests data or services | Provides data or services |
| Examples: Browser, mobile app | Examples: Web server, API server |
| Consumes APIs | Exposes APIs |

---

## Advantages

### 1. Centralized Data Management

Data can be stored and managed centrally on the server.

### 2. Easier Maintenance

Business logic can be updated on the server without requiring every client to manage the same logic.

### 3. Resource Sharing

Multiple clients can access the same services and resources.

### 4. Better Security Control

Authentication, authorization, and access control can be managed centrally.

### 5. Scalability

The architecture can evolve by adding more servers, caches, load balancers, and other components.

---

## Limitations

### 1. Server Can Become a Bottleneck

If too many clients send requests to one server, it may become overloaded.

```text
Thousands of Clients
        ↓
    One Server
        ↓
    Bottleneck
```

### 2. Single Point of Failure

If there is only one server and it crashes, the entire application may become unavailable.

### 3. Network Dependency

The client usually requires network connectivity to communicate with the server.

### 4. Increased Complexity at Scale

As traffic increases, additional components may be required:

- Load balancers
- Multiple servers
- Caches
- Database replicas
- Message queues

---

## Client-Server Architecture at Scale

A simple application may start like this:

```text
Client → Server → Database
```

As the application grows:

```text
Clients
   │
   ▼
Load Balancer
   │
   ├──► Server 1
   ├──► Server 2
   └──► Server 3
            │
            ▼
          Cache
            │
            ▼
         Database
```

The fundamental idea, however, remains the same:

> **Clients request services, and servers provide them.**

---

## Real-World Examples

### Web Application

```text
Browser → Web Server → Database
```

### Mobile Application

```text
Mobile App → API Server → Database
```

### E-Commerce Application

```text
Customer App
      ↓
Backend Server
      ↓
Product / Order / Payment Services
      ↓
Databases
```

---

## Important Trade-offs

### Centralization vs Dependency

Centralized servers make data and business logic easier to manage, but clients become dependent on the availability of those servers.

### Simplicity vs Scalability

A single server is simple to build and maintain, but it may not handle very large amounts of traffic.

### More Servers vs More Complexity

Adding servers improves scalability and availability, but introduces additional challenges such as:

- Load balancing
- Data consistency
- Session management
- Distributed system complexity

---

## Interview Takeaways

- A **client initiates a request**.
- A **server receives, processes, and responds to the request**.
- The client and server usually communicate over a **network**.
- The server may interact with databases, caches, and other services.
- A single server can serve multiple clients.
- As traffic grows, a single server can become a **bottleneck** or **single point of failure**.
- Client-server architecture is the foundation for many other System Design concepts.

---

## Quick Revision

> **Client-Server Architecture** is a model where a client requests data or services and a server processes the request and returns a response.

```text
Client
   │
   │ Request
   ▼
Server
   │
   │ Process
   ▼
Database / Other Services
   │
   │ Result
   ▼
Server
   │
   │ Response
   ▼
Client
```

### Remember

```text
Client = Requests a service
Server = Provides a service
```

The next question is:

> **How does the client find and communicate with the correct server?**

That leads to:

**IP Addresses → DNS → HTTP/HTTPS**

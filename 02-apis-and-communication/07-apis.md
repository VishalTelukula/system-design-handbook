## 7. APIs (Application Programming Interfaces)

An **API (Application Programming Interface)** is a contract that allows two software systems to communicate with each other.

It defines:

* **What** you can request
* **How** you should make the request
* **What** response you will receive

### How an API Works

```text
Client Application
        |
        | JSON Request
        v
    API Layer
        |
        |---- Authentication & Validation
        |
        |---- Business Logic
        |
        v
     Database
        |
        | JSON Response
        v
Client Application
```

The client sends a **request** to the API. The server processes the request, may interact with a database, and sends back a **response**.

### Real-World Analogy

Think of an API like a **restaurant**:

```text
Customer  →  Menu  →  Order  →  Kitchen  →  Food
Client    →  API   → Request →  Server   → Response
```

You do not go into the kitchen and prepare the food yourself.

Instead:

* The **menu** tells you what you can order → **API documentation**
* You place an order → **API request**
* The kitchen prepares it → **Server processes the request**
* You receive your food → **API response**

The client does not need to know how the server works internally.

### Example API Request

A client wants to get information about a user:

```http
GET /users/123
```

The server may return:

```json
{
  "id": 123,
  "name": "John",
  "email": "john@example.com"
}
```

Most modern web APIs commonly communicate using **JSON over HTTP**.

### Important API Components

#### Endpoint

An **endpoint** is a specific URL where an API resource can be accessed.

```http
GET /users
GET /users/123
GET /products
```

#### Request

A request is sent by the client and can contain:

* URL
* HTTP method
* Headers
* Authentication information
* Request body

#### Response

The server sends back a response containing:

* Status code
* Headers
* Data

Example:

```text
200 OK          → Request successful
201 Created     → Resource created
400 Bad Request → Invalid request
401 Unauthorized → Authentication required
404 Not Found   → Resource not found
500 Server Error → Server-side error
```

### Why APIs Are Useful

APIs allow different systems to communicate without needing to know each other's internal implementation.

For example:

```text
Mobile App ──┐
             |
Web App ─────┼──> API ───> Business Logic ───> Database
             |
Other Service┘
```

The same API can serve multiple clients.

### Common API Flow

```text
Client
   |
   | 1. Sends Request
   v
API Endpoint
   |
   | 2. Authentication & Validation
   v
Business Logic
   |
   | 3. Read/Write Data
   v
Database
   |
   | 4. Return Response
   v
Client
```

> Not all APIs are designed in the same way. Different API styles exist for different needs.

Two of the most popular API styles are **REST** and **GraphQL**.

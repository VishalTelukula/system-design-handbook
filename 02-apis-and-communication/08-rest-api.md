## 8. REST API

**REST (Representational State Transfer)** is one of the most commonly used architectural styles for building APIs on the web.

In REST, data is represented as **resources**, and each resource is identified by a unique URL, also called an **endpoint**. Clients interact with these resources using standard **HTTP methods** such as `GET`, `POST`, `PUT`, `PATCH`, and `DELETE`.

### Example: User Resource

Suppose an application has a `users` resource:

| HTTP Method | Endpoint     | Operation                    |
| ----------- | ------------ | ---------------------------- |
| `GET`       | `/users`     | Get all users                |
| `GET`       | `/users/123` | Get user with ID `123`       |
| `POST`      | `/users`     | Create a new user            |
| `PUT`       | `/users/123` | Replace or update user `123` |
| `PATCH`     | `/users/123` | Partially update user `123`  |
| `DELETE`    | `/users/123` | Delete user `123`            |

### REST and CRUD

REST maps naturally to **CRUD operations**:

| CRUD Operation | HTTP Method     | Purpose                     |
| -------------- | --------------- | --------------------------- |
| **Create**     | `POST`          | Create a new resource       |
| **Read**       | `GET`           | Retrieve a resource         |
| **Update**     | `PUT` / `PATCH` | Modify an existing resource |
| **Delete**     | `DELETE`        | Remove a resource           |

For example:

```http
GET /users/123
```

This retrieves the user whose ID is `123`.

```http
DELETE /users/123
```

This deletes the user whose ID is `123`.

The **URL identifies the resource**, while the **HTTP method defines the action** to perform on that resource.

---

### Key REST Principles

#### 1. Stateless

Each request must contain all the information required for the server to process it.

The server should not depend on information stored from a previous request.

For example:

```http
GET /users/123
Authorization: Bearer <token>
```

The request contains the authentication information needed to process it.

**Benefit:** Any server instance can handle any request, which makes horizontal scaling easier.

---

#### 2. Resource-Based URLs

REST APIs are designed around **resources**, usually represented using nouns.

**Good:**

```http
GET /users
GET /users/123
GET /users/123/orders
```

**Avoid:**

```http
GET /getUsers
POST /createUser
DELETE /deleteUser/123
```

The HTTP method already describes the action, so the URL should primarily describe the resource.

---

#### 3. Uniform Interface

REST APIs should follow consistent conventions.

For example:

```http
GET    /products
GET    /products/101
POST   /products
PATCH  /products/101
DELETE /products/101
```

A consistent structure makes the API easier to understand, use, and maintain.

---

#### 4. Cacheable

REST responses can be cached when appropriate.

For example:

```http
GET /products
```

If the product data does not change frequently, the response can be cached to reduce:

* Server load
* Database queries
* Network requests
* Response time

HTTP headers such as `Cache-Control`, `ETag`, and `Last-Modified` can be used to control caching behavior.

---

### Example REST Request and Response

#### Request

```http
GET /users/123
```

#### Response

```json
{
  "id": 123,
  "name": "John",
  "email": "john@example.com"
}
```

The server returns a representation of the requested resource, commonly in **JSON** format.

---

### Advantages of REST

* Simple and easy to understand
* Uses standard HTTP methods
* Works well with web and mobile applications
* Stateless architecture makes scaling easier
* Supports caching
* Widely adopted and supported
* Easy to test using tools such as Postman or `curl`

---

### Limitations of REST

One common limitation of REST is that the client may need to make **multiple API requests** to collect related data.

For example, imagine a page needs:

* User information
* User's posts
* User's followers

The client might need to make three separate requests:

```http
GET /users/123
GET /users/123/posts
GET /users/123/followers
```

This can lead to **over-fetching**, **under-fetching**, or multiple network round trips.

### Trade-off

REST provides **simplicity, predictability, and strong HTTP semantics**, but it may require multiple requests when the client needs complex or highly connected data.

This leads to an important question:

> **What if the client could request exactly the data it needs in a single request?**

That is one of the problems **GraphQL** was designed to solve.

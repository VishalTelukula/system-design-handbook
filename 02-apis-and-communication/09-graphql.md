## 9. GraphQL

**GraphQL** is an API query language originally developed by Facebook. It allows clients to request **exactly the data they need** in a single request.

Unlike REST, where the client may need to call multiple endpoints, GraphQL usually uses a **single endpoint** and lets the client specify the structure of the required data.

### Example

Suppose we need a user's name and their post titles.

With REST, we might make multiple requests:

```http
GET /users/123
GET /users/123/posts
```

With GraphQL, we can request everything in a single query:

```graphql
query {
  user(id: 123) {
    name
    posts {
      title
    }
  }
}
```

The server returns only the requested fields:

```json
{
  "data": {
    "user": {
      "name": "John",
      "posts": [
        {
          "title": "Understanding APIs"
        }
      ]
    }
  }
}
```

### How It Works

```text
Client
   |
   | Single GraphQL Query
   v
GraphQL Server
   |
   |----> Users Service
   |----> Posts Service
   |----> Comments Service
   |
   v
Combined Response
```

The **GraphQL server** receives the query, fetches the required data from different services or databases, and returns a combined response.

### REST vs GraphQL

| REST                              | GraphQL                               |
| --------------------------------- | ------------------------------------- |
| Multiple endpoints                | Usually a single endpoint             |
| Server decides response structure | Client chooses required fields        |
| May require multiple requests     | Can fetch related data in one request |
| Easier HTTP caching               | Caching can be more complex           |
| Simpler server implementation     | Requires schemas and resolvers        |

### Advantages

* Fetch exactly the required data
* Reduce unnecessary data transfer
* Fetch related resources in a single request
* Useful when different clients need different data

### Trade-offs

* More complex server-side implementation
* Requires **schemas and resolvers**
* Caching can be harder than REST
* Deeply nested queries can cause performance problems

### When to Use GraphQL

GraphQL is useful when clients need **flexible and complex data fetching**, such as:

* Social media applications
* Dashboards
* Mobile applications
* Applications with many related resources

For many system design problems, **REST is a simpler and safer default**. GraphQL is useful when clients need more control over exactly what data they receive.

> REST and GraphQL work well for request-response communication. But what if the server needs to send data to the client in real time?

This leads us to **WebSockets**.

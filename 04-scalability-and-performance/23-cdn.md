
## 25. CDN (Content Delivery Network)

A **CDN (Content Delivery Network)** is a network of servers located around the world that stores copies of your **static content** (images, CSS, JavaScript, videos) and serves it from the server closest to the user.

```text
            Origin Server
                 |
        -------------------
        |        |        |
     London   Mumbai  Singapore
      Edge      Edge      Edge
       |          |         |
   UK Users   India Users  SEA Users
```

Instead of every user requesting content from the origin server, they receive it from the **nearest edge server**, reducing latency.

### How It Works

1. User requests a file.
2. CDN checks if the file is cached.
3. **Cache Hit:** File is served from the nearest edge server.
4. **Cache Miss:** CDN fetches the file from the origin server, caches it, and serves it.

### Popular CDN Providers

- **Cloudflare**
- **Amazon CloudFront**
- **Akamai**

### Advantages

- Faster content delivery
- Lower latency
- Reduces load on the origin server
- Improves availability and scalability

### Trade-offs

- Cached content may become outdated.
- Cache invalidation can be challenging.
- Additional cost for CDN services.

> Use a CDN whenever your application serves static assets or media to users across different geographic locations.

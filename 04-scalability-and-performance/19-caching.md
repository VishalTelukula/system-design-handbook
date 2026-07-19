
## 16. Caching

**Caching** stores frequently accessed data in **fast memory** (such as Redis) so the application doesn't have to query the database every time.

```text
Client
   |
App Server
   |
Check Cache
   |
  Hit -------> Return Data
   |
  Miss
   |
Database
   |
Store in Cache
   |
Return Data
```

The most common caching pattern is **Cache-Aside (Lazy Loading)**:

1. Check the cache.
2. If data exists (**Cache Hit**), return it.
3. If not (**Cache Miss**), fetch it from the database.
4. Store the data in the cache.
5. Return it to the client.

### Popular Cache Technologies

- **Redis**
- **Memcached**

### Advantages

- Faster response times
- Reduces database load
- Improves application performance
- Handles high read traffic efficiently

### Trade-offs

- Cache can become stale if data changes.
- Cache invalidation adds complexity.

### Common Cache Invalidation Strategies

- **TTL (Time-To-Live):** Cache expires automatically after a set time.
- **Write-Through:** Update both the cache and database together.
- **Write-Behind:** Update the cache first, then the database asynchronously.

> Caching is one of the most effective ways to improve the read performance of a system.

# 6. HTTP / HTTPS

**HTTP (Hypertext Transfer Protocol)** is a protocol used for communication between a **client** and a **server** over the web.

When you visit a website:

1. The client sends an **HTTP request** to the server.
2. The server processes the request.
3. The server sends an **HTTP response** back to the client.

```text
Client → HTTP Request → Server
Client ← HTTP Response ← Server
```

## HTTP

With **HTTP**, the data sent between the client and server is **not encrypted**.

This means that someone who intercepts the communication may be able to read the data.

```text
Client ←── Unencrypted Data ──→ Server
```

HTTP commonly uses **port 80**.

## HTTPS

**HTTPS (Hypertext Transfer Protocol Secure)** is the secure version of HTTP.

It uses **TLS (Transport Layer Security)** to encrypt the communication between the client and server.

```text
Client ←── Encrypted Data ──→ Server
```

This helps protect sensitive information such as:

- Passwords
- Payment details
- Personal information

HTTPS commonly uses **port 443**.

## Key Difference

| HTTP | HTTPS |
|---|---|
| Data is not encrypted | Data is encrypted |
| Less secure | More secure |
| Uses port 80 | Uses port 443 |
| Uses HTTP | Uses HTTP with TLS |

> **HTTPS provides secure and encrypted communication between the client and server.**

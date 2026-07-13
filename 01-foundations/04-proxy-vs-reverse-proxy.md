# 4. Proxy / Reverse Proxy

When you visit a website, your request may pass through a **proxy** or **reverse proxy** before reaching the server.

## Proxy

A **proxy server** acts as a middleman between your device and the internet.

When you request a webpage, the proxy:

1. Receives your request.
2. Forwards it to the target server.
3. Gets the response from the server.
4. Sends the response back to you.

A proxy can hide your IP address, helping keep your location and identity private.

## Reverse Proxy

A **reverse proxy** acts as a middleman between clients and backend servers.

It receives client requests and forwards them to the appropriate backend server based on predefined rules.

A reverse proxy can:

- Hide backend server IP addresses.
- Control incoming traffic.
- Improve security by preventing direct access to backend servers.
- Act as a **load balancer** by distributing traffic across multiple servers.

## Key Difference

- **Proxy** → Works on behalf of the **client**.
- **Reverse Proxy** → Works on behalf of the **server**.

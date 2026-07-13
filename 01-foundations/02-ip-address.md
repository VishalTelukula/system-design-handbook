# 02. IP Address

An **IP Address (Internet Protocol Address)** is a unique numerical address used to identify and locate a device on a network.

## Why Do We Need an IP Address?

A client does not automatically know where a server is located. It needs an address to find and communicate with the correct server.

On the internet, computers identify each other using **IP addresses**, which work similarly to phone numbers.

When a client wants to communicate with a server, the request must be sent to the server's IP address.

## IPv4 and IPv6

### IPv4

IPv4 uses a **32-bit address**.

Example: `192.168.1.1`

IPv4 has a limited number of possible addresses, which became a problem as the number of internet-connected devices increased.

### IPv6

IPv6 uses a **128-bit address** and provides a much larger number of possible addresses.

Example: `2001:db8::1`

## Public and Private IP Addresses

### Public IP Address

A public IP address is used to identify a device or network on the public internet.

### Private IP Address

A private IP address is used inside a private network, such as a home, office, or cloud network.

## The Problem with IP Addresses

There are two major problems with using IP addresses directly:

1. **They are difficult to remember**  
   Users cannot be expected to memorize an IP address for every website or service.

2. **They can change**  
   If a service is moved to another server, its IP address may change and direct connections to the old IP address would stop working.

## The Solution: DNS

Instead of remembering IP addresses, we use human-readable domain names such as `google.com`.

The **Domain Name System (DNS)** translates a domain name into the IP address of the server.

For example:

`google.com` → DNS finds the IP address → Client connects to the server

## Quick Revision

- An **IP address** identifies and locates a device on a network.
- **IPv4** uses 32-bit addresses.
- **IPv6** uses 128-bit addresses.
- **Public IP addresses** are used on the public internet.
- **Private IP addresses** are used inside private networks.
- IP addresses are difficult to remember and may change.
- **DNS** allows us to use domain names instead of remembering IP addresses.

> **An IP address tells the network where the server is. DNS helps the client find that IP address using a human-readable domain name.**

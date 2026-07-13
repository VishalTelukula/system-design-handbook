# 03. DNS

**DNS (Domain Name System)** maps human-readable domain names to their corresponding IP addresses.

Instead of remembering hard-to-read IP addresses, we use domain names such as `github.com`.

## How Does DNS Work?

When you type `github.com` into your browser:

1. Your computer asks a **DNS server** for the corresponding IP address.
2. The DNS server returns the IP address associated with the domain.
3. Your browser uses that IP address to connect to the server and make a request.

## Finding the IP Address of a Domain

You can find the IP address associated with a domain using commands such as:

`ping github.com`

or

`nslookup github.com`

## Quick Revision

- **DNS** stands for **Domain Name System**.
- It maps **domain names** to **IP addresses**.
- It allows users to access websites using easy-to-remember names instead of numerical IP addresses.

> **DNS acts like the phonebook of the internet, translating domain names into IP addresses.**

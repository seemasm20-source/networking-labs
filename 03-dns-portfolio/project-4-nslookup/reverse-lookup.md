# 🔎 nslookup: Reverse Lookup

## 📋 What is a Reverse Lookup?

A **reverse lookup** resolves an **IP address** to its corresponding **hostname (domain name)**.

Instead of searching for the IP address of a hostname, the DNS server searches for a **PTR (Pointer) record** that maps the IP address back to the associated hostname.

---

## 🔧 How to Run

```cmd
C:\> nslookup 8.8.8.8
```

```text
Server:  dns.google         ← DNS server that answered
Address: 8.8.8.8            ← IP address of that DNS server

Name:    dns.google         ← hostname returned for the queried IP
Address: 8.8.8.8            ← IP address that was queried
```

In this example, the DNS server performs a reverse lookup by resolving the IP address `8.8.8.8` to the hostname `dns.google`.

> **Note:** The `Server` and `Name` lines are identical here because the IP being queried (`8.8.8.8`) is also the DNS server that answered. On a different network, `Server` shows your own DNS server, while `Name` still shows the hostname for the IP you looked up.

**Screenshot: nslookup 8.8.8.8:**

<img width="1920" height="1080" alt="Screenshot (364)" src="https://github.com/user-attachments/assets/c3972c97-c579-497b-b3f1-336fc2520f3a" />

---

## 📖 Reading the Output Line by Line

| Line | Meaning | Example |
|------|---------|---------|
| **Server** | The DNS server that responded to the query | `dns.google` |
| **Address** (first) | The IP address of the DNS server that responded | `8.8.8.8` |
| **Name** | The hostname returned by the PTR record for the queried IP | `dns.google` |
| **Address** (second) | The IP address that was queried | `8.8.8.8` |








THE END












































🔎 NSLOOKUP- Reverse Lookup


## What is it?

A reverse lookup is the process of resolving an IP address to its corresponding hostname (domain name).

Instead of searching for the IP address of a hostname, the DNS server searches for a PTR (Pointer) record

that maps the IP address back to the associated hostname.





## 🔧 How to Run


C:\> nslookup 8.8.8.8

Server:  dns.google

Address: 8.8.8.8

Name:    dns.google   ← hostname for that IP

Address: 8.8.8.8














<img width="1920" height="1080" alt="Screenshot (364)" src="https://github.com/user-attachments/assets/c3972c97-c579-497b-b3f1-336fc2520f3a" />

































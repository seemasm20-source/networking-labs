

# 🔍 nslookup: Forward Lookup

## 📋 What is a Forward Lookup?

A **forward lookup** resolves a **hostname (domain name)** to its corresponding **IP address**.

When a user enters a hostname such as `google.com`, the DNS server searches for the associated **A (IPv4)** or **AAAA (IPv6)** record and returns the IP address.

---

## 🔧 How to Run

```cmd
C:\> nslookup google.com
```

```text
Server:  dns.google             ← DNS server that answered
Address: 8.8.8.8                ← IP address of that DNS server

Non-authoritative answer:       ← answered by a resolver, not the domain's own DNS server
Name:    google.com             ← hostname that was queried
Address: 142.251.14.138         ← IP address returned
```

In this example, the DNS server performs a forward lookup by resolving the hostname `google.com` to its IPv4 address.

**Screenshot: nslookup google.com:**


---


## 📖 Reading the Output Line by Line

| Line | Meaning | Example |
|------|---------|---------|
| **Server** | The DNS server that responded to the query | `dns.google` |
| **Address** (first) | The IP address of the DNS server that responded | `8.8.8.8` |
| **Non-authoritative answer** | The answer came from a DNS server that is not the authoritative server for the domain, such as a recursive resolver or its cache | Shown in the output |
| **Name** | The hostname (domain name) that was queried | `google.com` |
| **Address** (second) | The IP address returned for the hostname. If several are returned, the label changes to **Addresses**, and the list can include both IPv4 (A) and IPv6 (AAAA) | `142.251.14.138` (IPv4) |





END IT HERE
















<img width="1920" height="1080" alt="Screenshot (363)" src="https://github.com/user-attachments/assets/b9beec96-15e8-4ddc-a9e5-966e439850b4" />


























## NSLOOKUP- Forward Lookup


 📋 What is it?


A **forward lookup** is the process of resolving a **hostname (domain name)** to its corresponding **IP address**.

When a user enters a hostname such as `google.com`, the DNS server searches for the associated **A (IPv4)** or

**AAAA (IPv6)** record and returns the corresponding IP address.



**Example:**

```cmd
nslookup google.com
```

**Result:**

```text
Name:    google.com
Address: 142.251.20.139
```

In this example, the DNS server performs a forward lookup by resolving the hostname `google.com` to its IPv4 address.





## 🔧 How to Run

C:\> nslookup google.com

Server:  dns.google         ← DNS server that answered

Address: 8.8.8.8

Non-authoritative answer:   ← answered from cache

Name:    google.com

Address: 142.251.14.138     ← IP returned



































<img width="1920" height="1080" alt="Screenshot (363)" src="https://github.com/user-attachments/assets/b9beec96-15e8-4ddc-a9e5-966e439850b4" />



























































































## 📖 Reading Output Line by Line



















| **Line**                     | **Meaning**                                                                                                                   | **Example**             |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| **Server**                   | The DNS server that responded to the query.                                                                                   | `dns.google`            |
| **Address**                  | The IP address of the DNS server that responded.                                                                              | `8.8.8.8`               |
| **Non-authoritative Answer** | The DNS server returned a cached or recursive response rather than responding as the authoritative DNS server for the domain. | `Yes`                   |
| **Name**                     | The hostname (domain name) that was queried.                                                                                  | `google.com`            |
| **Addresses**                | The IP address(es) returned by the DNS server. This may include both IPv4 (A records) and IPv6 (AAAA records).                | `142.251.14.138 ` (IPv4) |







→ [DNS Reverse Lookup](https://github.com/seemasm20-source/networking-labs/edit/main/03-dns-portfolio/project-4-nslookup/reverse-lookup.md)

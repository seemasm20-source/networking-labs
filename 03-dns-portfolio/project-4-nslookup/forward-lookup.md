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

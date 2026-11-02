# 📖 DNS Fundamentals

[← Back to DNS Portfolio README](../README.md)

---

## 💡 What is DNS?

DNS stands for Domain Name System. Every website has an IP address, for example 142.250.180.46.

Humans cannot remember number strings. DNS translates names into numbers.

```text
You type     : www.google.com
DNS converts : www.google.com → 142.250.180.46
Browser goes : to 142.250.180.46 → page loads
```

---

## 🔄 How DNS Works — Step by Step

1. You type `www.google.com` in the browser
2. The PC checks its local DNS cache first
3. If the answer is not cached, the PC asks its configured DNS server
4. The DNS server returns the IP: 142.250.180.46
5. The PC connects to that IP
6. The website loads

---

## 📚 Key DNS Terms

| Term | Short Description |
|------|-------------------|
| DNS Server | Answers "what IP is this name?" |
| A Record | Maps a hostname to an IPv4 address |
| CNAME | Alias: one name points to another |
| PTR Record | Reverse lookup: IP to name |
| DNS Cache | Saved answers from previous lookups |
| TTL | How long a DNS answer stays cached |
| Forward Lookup | Name → IP address |
| Reverse Lookup | IP address → Name |

---

## 🎯 Why DNS Matters for Tier 1

> **Key rule:** if ping by IP works but ping by name fails, the problem is DNS.

- Real scenarios with the user complaint and root cause: see the **DNS Troubleshooting Matrix** in the [portfolio README](../README.md)
- Commands used in the labs: [DNS Cheatsheet](../project-4-nslookup/dns-cheatsheet.md)

---

## 💡 Next Step

→ [Project 2: DNS Troubleshooting Lab](../project-2-troubleshooting/)

# 📋 DNS Commands Cheatsheet

[← Back to Project 2 README](./README.md)

---

## 🔑 Commands Quick Reference

| Command | What It Does |
|---------|--------------|
| `ipconfig /all` | Shows the full IP configuration, including the DNS server |
| `ipconfig /displaydns` | Shows all current DNS cache entries |
| `ipconfig /flushdns` | Clears all cached DNS entries |
| `nslookup hostname` | Forward lookup: name to IP |
| `nslookup IP` | Reverse lookup: IP to name |
| `nslookup hostname 8.8.8.8` | Queries a specific DNS server (here Google's) |
| `ping hostname` | Tests name resolution and connectivity |
| `ping IP` | Tests connectivity, bypassing DNS |

> **Key rules**
> - Ping by IP works but ping by name fails = DNS problem.
> - `nslookup` asks the DNS server directly and ignores the PC's cache. If `nslookup` works but `ping` or the browser fails, suspect a stale cache on that PC.

---

## 🚦 Troubleshooting Decision Flow

```text
User cannot open websites
│
├── ping 8.8.8.8 fails?
│   └── Internet connectivity problem, not DNS
│
├── ping 8.8.8.8 works + nslookup fails?
│   └── DNS server problem
│       → ipconfig /all → check the DNS server IP
│       → nslookup hostname 8.8.8.8
│
├── External works + internal fails?
│   └── Wrong DNS: using public, not internal
│       → Change DNS to the internal server IP
│
├── Specific hostname fails?
│   ├── nslookup returns Non-existent domain?
│   │   └── Missing A record → escalate to Tier 2
│   └── nslookup works but ping/browser fails?
│       └── Stale cache → ipconfig /flushdns
│
└── Some PCs work, others don't?
    └── Compare ipconfig /all on a working and a failing PC
        → Different DNS server? Correct it
        → Same DNS server? ipconfig /flushdns on the affected PCs
```

---

## ✅ Diagnostic Checklist

| Caller Says | First Command | Expected Finding |
|-------------|---------------|------------------|
| "I can't open any website" | `ping 8.8.8.8` | If it works, it is a DNS issue |
| "Only internal sites fail" | `ipconfig /all` | Wrong DNS server |
| "An old version of the site shows" | `ipconfig /displaydns` | Old IP in the cache |
| "The new server is unreachable by name" | `nslookup servername` | Non-existent domain |
| "It works for some staff, not others" | `ipconfig /all` on both PCs | Different DNS server, or a stale cache on one |
| "It broke after network changes" | `ipconfig /all` | DNS server IP changed |

---

## 💡 Next Step

→ [Project 3: DNS Cache Troubleshooting](../project-3-cache/)


## 📋 DNS Commands Cheatsheet

   

   
   
   All Commands- Quick Reference



| Command                   | What It Does                        |
| ------------------------- | ----------------------------------- |
| ipconfig /all             | Full config including DNS server IP |
| ipconfig /displaydns      | All current DNS cache entries       |
| ipconfig /flushdns        | Clears all cached DNS entries       |
| ipconfig /registerdns     | Re-registers PC with DNS server     |
| nslookup hostname         | Forward lookup — name to IP         |
| nslookup IP               | Reverse lookup — IP to name         |
| nslookup hostname 8.8.8.8 | Query Google DNS directly           |
| ping hostname             | Tests DNS + connectivity            |
| ping IP                   | Tests connectivity — bypasses DNS   |














## 🚦Troubleshooting Decision Flow



```
User cannot open websites
│
├── ping 8.8.8.8 fails?
│   └── Internet connectivity problem — not DNS
│
├── ping 8.8.8.8 works + nslookup fails?
│   └── DNS server problem
│       → ipconfig /all → check DNS server IP
│       → nslookup hostname 8.8.8.8
│
├── External works + internal fails?
│   └── Wrong DNS — using public not internal
│       → Change DNS to internal server IP
│
├── Specific hostname fails?
│   ├── nslookup returns Non-existent domain?
│   │   └── Missing A Record — escalate Tier 2
│   └── nslookup works but browser fails?
│       └── Stale cache → ipconfig /flushdns
│
└── Some PCs work — others don't?
    └── Cache difference
        → ipconfig /flushdns on affected PCs
```

---
















## Diagnostic Checklist




 | Caller Says                     | First Command        | Expected Finding       |
| ------------------------------- | -------------------- | ---------------------- |
| Cannot Open Any Website         | ping 8.8.8.8         | If Works → DNS Issue   |
| Only Internal Sites Fail        | ipconfig /all        | Wrong DNS Server       |
| Old Website Version Showing     | ipconfig /displaydns | Old IP In Cache        |
| New Server Unreachable By Name  | nslookup servername  | Non-existent Domain    |
| Works For Some Staff Not Others | ipconfig /displaydns | Stale Cache Difference |
| Broke After Network Changes     | ipconfig /all        | DNS Server IP Changed  |

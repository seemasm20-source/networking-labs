
# 🔴 Scenario 4 - DNS Service Down

[ Back to Project 2 README] → README.md



---

> **Lab Note:** An enterprise DNS server outage cannot be reproduced in a home lab. The client-side commands below show the standard troubleshooting method. Only the public-DNS test (Test 4) was run on a real machine. The other results are what a technician would expect on a production network. The internal DNS address is fictional.

## 📋 Problem Summary

Multiple users across the office cannot open any website or reach any server by name. The issue started suddenly and affects everyone. Ping by IP still works.

---


## 💡 What is a DNS Server Outage?

When the company's DNS server is offline or its DNS service has stopped, every PC that depends on it loses name resolution at the same time. The network itself still works, so ping by IP succeeds.

| | Scenario 2: Wrong DNS Server | Scenario 5: DNS Service Down |
|---|---|---|
| **Users affected** | One PC | The whole office |
| **Cause** | The PC points to a wrong server | The correct DNS server stopped working |
| **Who fixes it** | Tier 1 corrects the PC setting | Tier 2 / Infrastructure restores the server |

> **First triage question:** how many users are affected? One user points to the PC. Everyone points to the DNS server.

---

## 🔎 Verify the Problem

| Test | Command | Result | Meaning |
|------|---------|--------|---------|
| 1. Resolve a name | `nslookup google.com` | Timed out | The configured DNS server does not respond |
| 2. Check connectivity | `ping 8.8.8.8` | Reply | The network and internet are working |
| 3. Reach the DNS server | `ping 192.168.10.5` | Request timed out (expected) | The DNS server is unreachable |
| 4. Use a public DNS server | `nslookup google.com 8.8.8.8` | Resolves | DNS works elsewhere, so the fault is the company DNS server |


```text
C:\> nslookup google.com
DNS request timed out.
*** Can't find server name for address 192.168.10.5: Timed out

C:\> nslookup google.com 8.8.8.8
Server:  dns.google
Address: 8.8.8.8

Non-authoritative answer:
Name:    google.com
Addresses: <as shown in your screenshot>
```

> Tests 1 to 3 are expected results. Test 4 was run on a real machine.

**Screenshot: nslookup google.com 8.8.8.8 resolving successfully:**






<img width="1920" height="1080" alt="Screenshot (358)" src="https://github.com/user-attachments/assets/72d0c36a-c203-4845-9304-a4ff36483dbf" />











---


## 🔧 Fix

Before escalating, a IT Support team can check whether the PC has a secondary DNS server configured (`ipconfig /all`). If there is none and the primary does not respond, escalate to next level.

**Escalation details:**

| Field | Value |
|-------|-------|
| **Issue** | Configured internal DNS server unreachable |
| **Impact** | Multiple users across the office |
| **Confirmed** | `ping 192.168.10.5` timed out |
| **Isolation test** | `nslookup google.com 8.8.8.8` resolved, so the fault is the company DNS server |
| **Started** | Time of the first report |


---

## ✅ Verification

After Network Engineer restores DNS, repeat the tests (expected results):

| Command | Expected Result |
|---------|-----------------|
| `ping 192.168.10.5` | DNS server reachable |
| `nslookup google.com` | Resolves through the company DNS server |
| `ping google.com` | The name resolves and the destination replies |

---


## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | No hostname resolves across the office |
| **Cause** | The company DNS server is unavailable, or the DNS service has stopped |
| **Symptom** | All users affected; names fail, but ping by IP works |
| **Diagnose** | `nslookup google.com` timed out on the company DNS server; `nslookup google.com 8.8.8.8` resolved, isolating the fault |
| **Fix** | Escalated to Tier 2 / Infrastructure to restore the DNS service |
| **Verified** | Expected: the DNS server is reachable and names resolve again |

---

## 💡 Next Step

→ [DNS Cheatsheet](./dns-cheatsheet.md)







































                                                                               |


























 

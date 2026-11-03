
# 🔴 Scenario 3 - Internal vs External DNS

[ Back to Project 2 README] → [README.md](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-2-troubleshooting/README.md)

---


> **Lab Note:** This is a simulated enterprise DNS scenario. The internal domain names and IP addresses are fictional, and the home lab has no internal DNS infrastructure. The scenario shows the troubleshooting method. The fix and verification results are marked as expected, because they need an organisation's Active Directory DNS server.

## 📋 Problem Summary

  A user can open external websites such as google.com, but cannot reach the company intranet or internal servers by name. Multiple users on the same floor are affected.

---


## 💡 Internal vs External DNS

| | External (public) DNS | Internal (company) DNS |
|---|---|---|
| **Example** | 8.8.8.8 | 192.168.10.5 |
| **Knows** | Public websites | Internal names such as `intranet.company.local` |
| **Result for internal names** | Non-existent domain | Resolves correctly |

A PC that uses only a public DNS server can browse the internet but cannot resolve internal hostnames.

---


## 🔧 Create the Problem

   Point the PC at a public DNS server:

1. **Windows + I** → **Network & Internet** → your connection → **Hardware properties**
2. Next to **DNS server assignment**, click **Edit** → **Manual** → turn on **IPv4**
3. Preferred DNS: `8.8.8.8` → **Save**

---


## 🔎 Verify the Problem

```text
C:\> nslookup google.com
Address: <public IP>                  ← external DNS works

C:\> nslookup intranet.company.local
*** can't find intranet.company.local: Non-existent domain
```




<img width="1920" height="1080" alt="Screenshot (355)" src="https://github.com/user-attachments/assets/80466807-050e-474a-85f4-f9eebcfcec1d" />






---

| Test | Result | Meaning |
|------|--------|---------|
| `nslookup google.com` | Resolves | The public DNS server works |
| `nslookup intranet.company.local` | Non-existent domain | The public DNS server has no internal records |

> External names work and internal names fail, so the PC is using the wrong DNS server.

**Screenshot: nslookup for google.com (works) and intranet.company.local (fails):**

---


## 🔧 Fix

  Change the PC to use the company's internal DNS server:

| Setting | Value |
|---------|-------|
| **Preferred DNS** | 192.168.10.5 (internal DNS server) |


## ✅ Verification

After the DNS server is changed (expected results):

```text
C:\> ipconfig /flushdns
C:\> ipconfig /all
C:\> nslookup intranet.company.local
C:\> nslookup google.com
```


| Command | Expected Result |
|---------|-----------------|
| `ipconfig /flushdns` | Clears the cached failed lookups, so the new DNS server is used |
| `ipconfig /all` | DNS server shows 192.168.10.5 |
| `nslookup intranet.company.local` | Resolves to the intranet's IP |
| `nslookup google.com` | Still resolves (the internal DNS forwards external names) |

---

## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | Intranet unreachable while external websites work |
| **Cause** | Client used a public DNS server, which has no internal records |
| **Symptom** | `google.com` resolves; `intranet.company.local` fails |
| **Diagnose** | `nslookup intranet.company.local` returned Non-existent domain |
| **Fix** | Pointed the client to the internal DNS server (192.168.10.5) |
| **Verified** | Expected: internal and external names both resolve (needs a production DNS) |

---

## 💡 Next Step

→ [Scenario 4: Hostname Not Resolving](./hostname-not-resolving.md)




















































































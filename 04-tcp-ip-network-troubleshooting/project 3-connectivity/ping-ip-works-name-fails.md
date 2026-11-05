# 🔴 Connectivity 2 - Ping IP Works, Name Fails

[ Back to Project README] → [TCP/IP Network Troubleshooting - README.md](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/README.md)

---

## 📋 Problem Summary

A user can ping `8.8.8.8` successfully but cannot open any website by name. Internet connectivity is working, but DNS is not.

---




## 💡 What is a Name Resolution Failure?

Websites are reached by name, and DNS translates each name into an IP address. If the PC's DNS server is wrong or unreachable, the network still works, so ping by IP succeeds, but names fail.

| Symptom | Detail |
|---------|--------|
| Ping by IP works | The network and internet connection are fine |
| Ping by name fails | The name cannot be resolved to an IP address |
| No websites open | Browsers need DNS to find every site |

> **First check:** ping a public IP, then ping a name. If only the name fails, the fault is DNS.



---



## 🔎 Verify the Problem

| Test | Command | Result | Meaning |
|------|---------|--------|---------|
| 1. Test IP connectivity | `ping 8.8.8.8` | Reply | Basic IP connectivity works and the PC can reach external networks |
| 2. Test name resolution | `ping google.com` | Failed | The name cannot be resolved, so DNS is the suspect |
| 3. Check the DNS configuration | `ipconfig /all` | Check the DNS server address | Shows which DNS server the adapter is using |
| 4. Test DNS directly | `nslookup google.com` | Timed out | The configured DNS server is unreachable or incorrect |



**Screenshot: ping by IP works, ping by name fails:**



<img width="1920" height="1080" alt="ping 8.8.8.8 succeeding and ping google.com failing" src="https://github.com/user-attachments/assets/57434cd4-770c-4aa2-a914-60a411a28287" />







**Screenshot: `nslookup google.com` timing out:**



<img width="1920" height="1080" alt="nslookup google.com showing a DNS request timeout" src="https://github.com/user-attachments/assets/1a068f32-bb39-460b-9c5a-8acc27c60bb9" />



---



## 🔧 Fix

Set a valid DNS server or return the adapter to **Automatic (DHCP)**:


**Settings → Network & internet → Wi-Fi → Hardware properties → DNS server assignment → Edit**

| Setting | Value |
|---------|-------|
| Preferred DNS | from 0.0.0.0 to `8.8.8.8` |
| Alternate DNS | `8.8.4.4` |

For the full DNS troubleshooting guide, see the [DNS Troubleshooting Labs](https://github.com/seemasm20-source/networking-labs/tree/main/03-dns-portfolio/project-2-troubleshooting).



---



## ✅ Verification

| Command | Result | Meaning |
|---------|--------|---------|
| `nslookup google.com` | Resolves to an IP address ✅ | The DNS server responds |
| `ping google.com` | Reply ✅ | Name resolution and connectivity work |



**Screenshot: name resolution restored:**



<img width="1920" height="1080" alt="nslookup and ping google.com succeeding after the DNS fix" src="https://github.com/user-attachments/assets/741125db-9596-4245-ba88-d0f25a159263" />



---





## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | Ping by IP works, but websites cannot be opened by name |
| **Cause** | The configured DNS server is unreachable or incorrect |
| **Symptom** | `ping 8.8.8.8` replies; `ping google.com` fails; `nslookup` times out |
| **Diagnose** | Comparing ping by IP with ping by name, then `nslookup google.com` timing out |
| **Fix** | Set a valid DNS server (`8.8.8.8` / `8.8.4.4`) or returned to Automatic (DHCP) |
| **Verified** | `nslookup google.com` resolved; `ping google.com` replied |

---



## 💡 Next Step

→ [Connectivity 3](./connectivity-3.md)

































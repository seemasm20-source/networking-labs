# 🔴 Troubleshooting Issue 1 - APIPA (169.254.x.x)




 [ Back to Project README](../README.md) → [DHCP Configuration — GitHub README](https://github.com/seemasm20-source/networking-labs/blob/main/02-dhcp-configuration/README.md)






---



## 📋 Problem Summary

PCs in the HR Department (LAN 1) showed an APIPA address (169.254.x.x) with no network access. The DHCP service on the router was disabled, so no IP addresses were assigned automatically.




---




## 💡 What is APIPA?

When a PC cannot reach a DHCP server, it assigns itself a temporary 169.254.x.x address (Automatic Private IP Addressing). This address only works on the local segment. There is no default gateway, so the PC cannot reach other networks or the internet.

```text
DHCP disabled → no lease received → PC self-assigns 169.254.x.x → no network access
```

---



## 🔧 Create the Problem

Disable the DHCP service on the router:

```text
Router> enable
Router# configure terminal
Router(config)# no service dhcp
Router(config)# end
```

Then make the affected PC request a new address: **Desktop → IP Configuration**, click **Static**, then **DHCP** again.











*Screenshot: DHCP service disabled on the router:**



<img width="1920" height="1080" alt="Screenshot (304)" src="https://github.com/user-attachments/assets/062ca100-c944-4172-b915-140c56ebd14c" />








































---




 ## Impact:

DHCP disabled → No IP address lease received → Windows assigns an APIPA address (`169.254.x.x`) → Network connectivity is limited or unavailable.


















<img width="1920" height="1080" alt="Screenshot (302)" src="https://github.com/user-attachments/assets/efa1df4b-a0bd-45a7-8faa-74aa00e13579" />
























































## 🔎 Verify the Problem

On the affected PC: **Desktop → Command Prompt**

```text
PC> ipconfig
```

| Field | Value Seen |
|-------|------------|
| IP Address | 169.254.x.x (APIPA) |
| Default Gateway | empty |

> **Symptom:** 169.254.x.x + empty gateway = the PC could not get a lease from a DHCP server.

**Screenshot: PC showing the APIPA address:**





















<img width="1920" height="1080" alt="Screenshot (303)" src="https://github.com/user-attachments/assets/2ae09b4c-d991-470a-9543-6850ff8eeab6" />





















---

## 🔧 Fix

Restore the DHCP service and recreate the LAN 1 pool:

```text
Router> enable
Router# configure terminal

! --- Fix APIPA issue ---
Router(config)# service dhcp

! --- Recreate pool for LAN 1 ---
Router(config)# ip dhcp pool LAN1_POOL
Router(dhcp-config)# network 192.168.10.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.10.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit
Router(config)# end
Router# write memory
```

**Screenshot: DHCP service re-enabled and pool recreated:**






















<img width="1920" height="1080" alt="Screenshot (305)" src="https://github.com/user-attachments/assets/64185be0-9b54-4d62-b3e6-c8dcf1d162a6" />


























































✅ Renew IP on the PC:

ipconfig /release

ipconfig /renew

ipconfig

Expected after fix:

IPv4 Address   : 192.168.10.10  

Subnet Mask   : 255.255.255.0

Default Gateway: 192.168.10.1


















<img width="1920" height="1080" alt="Screenshot (306)" src="https://github.com/user-attachments/assets/0bd7f3cb-0106-4d6a-bf49-894572c293e6" />





















































<img width="1920" height="1080" alt="Screenshot (307)" src="https://github.com/user-attachments/assets/dbd1df9e-ab8f-4bff-85cb-1fee57756f93" />















































## 📋 Quick Summary Table:














































| Step             | Command / Action                     | Purpose                                                                                                     |
| ---------------- | ------------------------------------ | ----------------------------------------------------------------------------------------------------------- |
| Create Problem   | no service dhcp                      | Disables the DHCP service on the router, preventing clients from obtaining IP addresses automatically.      |
| Verify Issue     | ipconfig (on PC)                     | Checks the client's IP configuration and confirms whether an APIPA address (169.254.x.x) has been assigned. |
| Fix Problem      | service dhcp + recreate DHCP pool    | Re-enables the DHCP service and restores the DHCP configuration.                                            |
| Renew IP Address |ipconfig /release then ipconfig /renew| Releases the current IP address and requests a new lease                                                  |


















REAL WORLD TICKET:







User complaint

"My PC shows Limited Connectivity. Cannot access internet or shared drives."

Root cause

DHCP service disabled. PC self-assigned 169.254.x.x - unable to communicate.

Resolution

Re-enabled DHCP + recreated pool. Ran ipconfig /renew. IP 192.168.10.10 assigned — connectivity restored.






























# 🔴 Troubleshooting Issue 1 - APIPA (169.254.x.x)




  [ Back to Project README](../README.md) → [DHCP Configuration — GitHub README](https://github.com/seemasm20-source/networking-labs/blob/main/02-dhcp-configuration/README.md)






---



## 📋 Problem Summary

 PCs in the HR Department (LAN 1) showed an APIPA address (169.254.x.x) with no network access. The DHCP service on the router was disabled, so no IP addresses were assigned automatically.




---




## 💡 What is APIPA?

 When a PC cannot reach a DHCP server, it assigns itself a temporary 169.254.x.x address (Automatic Private IP Addressing). This address only works on the local segment. There is no    default gateway, so the PC cannot reach other networks or the internet.

```text
DHCP disabled → no lease received → PC self-assigns 169.254.x.x → no network access
```

---



## 🔧 Create the Problem

 Disable the DHCP service on the router:

```text
Router> enable
Router# configure terminal
Router(config)# no ip dhcp pool LAN1_POOL
Router(config)# end
```

Then make the affected PC request a new address: **Desktop → IP Configuration**, click **Static**, then **DHCP** again.











*Screenshot: DHCP service disabled on the router:**



<img width="1920" height="1080" alt="Screenshot (304)" src="https://github.com/user-attachments/assets/062ca100-c944-4172-b915-140c56ebd14c" />








































---

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





















<img width="1920" height="1080" alt="Screenshot (302)" src="https://github.com/user-attachments/assets/efa1df4b-a0bd-45a7-8faa-74aa00e13579" />














































































---

## 🔧 Fix

 ### Step 1 :  Restore the DHCP service and recreate the LAN 1 pool

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


























































### Step 2 - Renew the IP address on the PC

```text
PC> ipconfig /release
PC> ipconfig /renew
PC> ipconfig
```

**Result after fix:**

| Field | Value Received |
|-------|----------------|
| IP Address | 192.168.10.10 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.10.1 |

















<img width="1920" height="1080" alt="Screenshot (306)" src="https://github.com/user-attachments/assets/0bd7f3cb-0106-4d6a-bf49-894572c293e6" />































































































# ✅ Verification

After the renew, the PC received a valid address from the DHCP pool:

| Field | Value Received |
|-------|----------------|
| IP Address | 192.168.10.10 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.10.1 |

**Screenshot: PC with the correct DHCP-assigned address:**






















<img width="1920" height="1080" alt="Screenshot (307)" src="https://github.com/user-attachments/assets/51829b21-98ca-433e-ba6c-ba595bcbf21b" />






















---

## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | PCs showing APIPA address (169.254.x.x) |
| **Cause** | DHCP service disabled on the router |
| **Symptom** | 169.254.x.x address, empty default gateway, no network access |
| **Diagnose** | `ipconfig` on the PC shows an APIPA address |
| **Fix** | `service dhcp` on the router, then `ipconfig /release` and `/renew` on the PC |
| **Verified** | PC received 192.168.10.10 with gateway 192.168.10.1 |

---

## 💡 Next Step

 [DHCP Pool Exhaustion] →[DHCP Pool Exhaustion Issue](https://github.com/seemasm20-source/networking-labs/blob/main/02-dhcp-configuration/troubleshooting/dhcp-pool-exhaustion.md)
















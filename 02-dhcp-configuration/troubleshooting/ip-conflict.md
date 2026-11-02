
# 🔴 Troubleshooting Issue 3 - IP Address Conflict



 [ Back to Project README](../README.md) → [DHCP Configuration — GitHub README](https://github.com/seemasm20-source/networking-labs/blob/main/02-dhcp-configuration/README.md)


 ---

## 📋 Problem Summary

PC2 was manually assigned the static IP 192.168.10.10, the same address DHCP had already assigned to PC1. The duplicate address caused intermittent connection failures for both devices.

---






## 💡 What is an IP Address Conflict?

An IP address conflict occurs when two devices on the same network use the same IP address. The network cannot tell which device should receive the traffic, so connections drop or become unreliable.

It commonly happens when a static IP is set inside the range that DHCP also hands out.


---






## 🔧 Create the Problem

### Step 1 - Baseline: PC1 gets its address from DHCP

DHCP is configured as in [DHCP Configuration](../config/dhcp-config.md).

On PC1: **Desktop → IP Configuration → DHCP**, then check the result:

```text
PC1> ipconfig /all
```

| Field | Value |
|-------|-------|
| IP Address | 192.168.10.10 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.10.1 |

The address belongs to the 192.168.10.0/24 network and was assigned automatically by DHCP.

**Screenshot: PC1 with the DHCP-assigned address:**





<img width="1920" height="1080" alt="Screenshot (307)" src="https://github.com/user-attachments/assets/d55d4ef9-c865-4028-80e0-2dc2b55185c7" />





---

### Step 2 - Set the same address statically on PC2

On PC2: **Desktop → IP Configuration → Static**

```text
IP Address      : 192.168.10.10
Subnet Mask     : 255.255.255.0
Default Gateway : 192.168.10.1
DNS Server      : 8.8.8.8
```

Both devices now use the same address:

```text
PC1 = 192.168.10.10  (assigned by DHCP)
PC2 = 192.168.10.10  (configured manually)
```

**Screenshot: PC2 static IP configuration:**



<img width="1920" height="1080" alt="Screenshot (309)" src="https://github.com/user-attachments/assets/25d3edb5-d296-45a8-b609-d85c1402607c" />






---





## 🔎 Verify the Problem

On both PCs, open **Command Prompt** and run:

```text
PC> ipconfig /all
```

| Device | IPv4 Address |
|--------|--------------|
| PC1 | 192.168.10.10 |
| PC2 | 192.168.10.10 |

> Both devices are using the same IP address. This is the conflict.

**Screenshot: ipconfig /all on both PCs showing 192.168.10.10:**





<img width="1920" height="1080" alt="Screenshot (314)" src="https://github.com/user-attachments/assets/2a95488d-d204-4212-9fa8-c1617d010225" />










---






## 🔧 Fix

Change PC2 from a static configuration to DHCP:

**PC2 → Desktop → IP Configuration → DHCP**

The router's DHCP server assigns PC2 the next available address from the pool.

**Screenshot: PC2 switched to DHCP:**

> **Prevention:** Give statically configured devices an address from the excluded range (.1 – .9). DHCP never leases those, so they cannot clash with a client.


<img width="1920" height="1080" alt="Screenshot (312)" src="https://github.com/user-attachments/assets/bca70cea-2ac7-4fe1-8988-856c53f5cf29" />







---







## ✅ Verification

### Verification 1 - Unique IP addresses

```text
PC> ipconfig /all
```

| Device | IPv4 Address |
|--------|--------------|
| PC1 | 192.168.10.10 |
| PC2 | 192.168.10.11 |

**Screenshot: ipconfig /all showing unique addresses:**






<img width="1920" height="1080" alt="Screenshot (313)" src="https://github.com/user-attachments/assets/a77126ca-b10f-4724-81bf-7a4ca4a9ee9f" />






---

### Verification 2 - Connectivity

From PC2, ping the default gateway:

```text
PC2> ping 192.168.10.1
```

Result: four replies from 192.168.10.1, no packet loss.

**Screenshot: successful ping to 192.168.10.1:**




<img width="1920" height="1080" alt="Screenshot (313)" src="https://github.com/user-attachments/assets/a77126ca-b10f-4724-81bf-7a4ca4a9ee9f" />






---


## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | PC1 and PC2 used the same IP address (192.168.10.10) |
| **Cause** | PC2 was set to a static IP already leased by DHCP to PC1 |
| **Symptom** | Intermittent connectivity, random drops, unreliable communication |
| **Diagnose** | `ipconfig /all` on both PCs showed the same IPv4 address |
| **Fix** | Changed PC2 from static to DHCP, which gave it 192.168.10.11 |
| **Verified** | Unique addresses on both PCs; ping to 192.168.10.1 successful |

---
























































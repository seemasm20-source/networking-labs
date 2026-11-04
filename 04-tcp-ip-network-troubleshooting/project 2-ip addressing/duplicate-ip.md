
# 🔴 IP issue 5 - IP Address Conflict (Duplicate IP)

[ Back to Project 2 README] → [README.md](./README.md)

---

## 📋 Problem Summary

Two devices on the same network are using the same IP address. Both can experience intermittent connectivity drops, random failures and unreliable pings, because replies may reach either device. Windows may also show an "IP address conflict" warning.

---

## 💡 Quick Overview

| Symptom | Detail |
|---------|--------|
| Random connectivity drops | The connection works, then fails |
| Inconsistent ping replies | Some pings reply and some time out |
| One or both devices affected | Depends on which device answers first |
| Issue clears and returns | Often after a restart or lease renewal |

**Common causes:**

- A static IP assigned inside the DHCP pool range
- Two devices manually given the same static IP
- The DHCP excluded-address range is too small, so DHCP leases an address already used by a static device

---

## 🔎 Verify the Problem

### Step 1 - Check the IP configuration

```text
C:\> ipconfig /all
```

Check the IPv4 address, subnet mask, default gateway and whether DHCP is enabled, to see if the device uses a static address inside the DHCP range.

### Step 2 - Check the ARP table

```text
C:\> ping 192.168.10.50
C:\> arp -a
```

`arp -a` shows the IP-to-MAC mappings stored in the ARP cache. If the suspected IP address maps to a different MAC address at different times, another device is using the same IP.

---

## 🔧 Initial Troubleshooting (Tier 1)

Change one device to a unique address:

- Set the PC to **DHCP**, then run `ipconfig /release` and `ipconfig /renew`
- Or assign a different static IP that is not in use

**If the other device cannot be found, or the conflict returns → escalate to Tier 2.**

---

## ⬆️ Escalation: Tier 1 to Tier 2

| Field | Value |
|-------|-------|
| **Issue** | IP address conflict on the network |
| **Impact** | One or both devices, with intermittent connectivity |
| **Confirmed** | `arp -a` shows the same IP with different MAC addresses |
| **Tier 1 steps done** | `ipconfig /all`, `arp -a`, PC switched to DHCP or a new static IP |
| **Started** | Time of the first report |

---

## 🛠️ Tier 2 Investigation and Fix

| Check | Command or action | What it shows |
|-------|-------------------|---------------|
| Find the other device | Match the MAC from `arp -a` to a device (switch MAC table or device label) | Which device holds the duplicate IP |
| Check DHCP leases | `show ip dhcp binding` | Whether DHCP issued the address |
| Check the excluded range | `show running-config \| include excluded` | Whether static addresses are protected |

**Fix (Tier 2):**

- Move the static device to an address outside the DHCP pool, or reserve it
- Expand the excluded range so DHCP never leases static addresses
- Record static IP assignments to avoid repeats

---

## 🔗 Full Lab Documentation

This scenario was fully documented in the DHCP Configuration Portfolio, including:

- ✅ Complete Packet Tracer lab setup
- ✅ How to create the duplicate IP conflict
- ✅ Step-by-step fix with CLI commands
- ✅ Verification screenshots
- ✅ Real-world help desk ticket

→ View the full lab here: [IP Address Conflict (Static vs DHCP) Troubleshooting Lab](https://github.com/seemasm20-source/networking-labs/blob/main/02-dhcp-configuration/troubleshooting/ip-conflict.md)

























































---
## 🔴 IP Issue 5 - Duplicate IP Address





## 📋 Problem Summary

Two devices on the same network share the same IP address. Both experience intermittent connectivity

drops, random failures and unreliable pings. The network cannot determine which device to send replies to.





##  🔍 Quick Overview



Duplicate IP symptoms:

→ Random connectivity drops

→ Ping replies inconsistent

→ One or both devices affected

→ Issue clears temporarily then returns

Common causes:

→ Static IP assigned within DHCP pool range

→ One device manually given same static IP

→ DHCP excluded-address range too small





## 🔎 Quick Verify

### Step 1: Check the IP Configuration

Open the Command Prompt on each PC and run:

`ipconfig /all`

Check the IPv4 address, subnet mask, default gateway, and DHCP status to identify whether the devices are using the same IP address.

### Step 2: Check the ARP Table

Run:

`arp -a`

This command displays the IP-to-MAC address mappings stored in the ARP cache. If a suspected IP address is associated with 

different MAC addresses at different times,it may indicate a duplicate IP address conflict.



## 🔧 Quick Fix


Change one device to a unique IP:

→ Set to DHCP to receive unique IP automatically

→ OR assign different static IP not in use





## 🔗 Full Lab Documentation

This scenario was fully documented in the DHCP Configuration Portfolio including:

✅ Complete Packet Tracer lab setup

✅ How to create the duplicate IP conflict

✅ Step-by-step fix with CLI commands

✅ Verification screenshots

✅ Real-world help desk ticket
              
→ View full lab here:


[IP Address Conflict (Static vs DHCP) Troubleshooting Lab](https://github.com/seemasm20-source/networking-labs/blob/main/02-dhcp-configuration/troubleshooting/ip-conflict.md)

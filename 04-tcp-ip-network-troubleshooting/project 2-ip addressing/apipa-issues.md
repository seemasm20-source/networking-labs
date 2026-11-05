# 🔴 IP Issue 4 - APIPA (169.254.x.x)

[ Back to Project 2 README] → [TCP/IP Network Troubleshooting - README.md](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/README.md)

---

## 📋 Problem Summary

A PC shows an IP address starting with `169.254.x.x` and has no network or internet access. The PC could not reach a DHCP server, so Windows gave itself an APIPA address.

---

## 💡 Quick Overview

APIPA (Automatic Private IP Addressing) activates automatically on Windows when a PC set to DHCP cannot reach a DHCP server. The PC assigns itself an address from the `169.254.0.0/16` range.

This address is a self-assigned fallback only. It cannot reach the gateway, other networks or the internet. It can only talk to other APIPA devices on the same local network.

| Sign | Meaning |
|------|---------|
| `169.254.x.x` | APIPA address |
| Subnet mask `255.255.0.0` | Default mask for the APIPA range |
| Empty default gateway | The PC never received DHCP settings |
| No network or internet access | The PC is isolated from the rest of the network |

---

## 🔎 Verify the Problem

```text
C:\> ipconfig

Autoconfiguration IPv4 Address. . : 169.254.45.78   ← APIPA!
Subnet Mask . . . . . . . . . . . : 255.255.0.0
Default Gateway . . . . . . . . . :                  ← empty
```

```text
C:\> ping 192.168.10.1
Request timed out.   ❌
```

> The ping result can also show "Destination host unreachable" or "General failure". All of them mean the gateway cannot be reached.

---

## 🔧 Basic Troubleshooting (Tier 1)

```text
C:\> ipconfig /release
C:\> ipconfig /renew
```

If the PC still shows an APIPA address:

1. Check that the network cable is connected, or that Wi-Fi is connected to the right network
2. Check that the switch port is active
3. Check whether other PCs on the same network also have `169.254.x.x` addresses

---

## ⬆️ Investigation (Tier 2)

If the PC still shows APIPA after the Tier 1 steps or several PCs are affected, escalate.

| Field | Value |
|-------|-------|
| **Issue** | PC has a `169.254.x.x` address and cannot get a DHCP lease |
| **Impact** | One PC or multiple PCs on the same network |
| **Confirmed** | `ipconfig` shows APIPA and the gateway ping times out |
| **Tier 1 steps done** | `ipconfig /release`, `ipconfig /renew`, cable and switch port checked |
| **Tier 2 checks** | DHCP service running, DHCP scope not exhausted, DHCP reachable from the VLAN |

> **First triage question:** how many users are affected? One PC points to the PC, cable or port. Many PCs point to the DHCP server.


**Common Tier 2 fixes:**

- Re-enable the service with `service dhcp`
- Recreate or correct the DHCP pool
- Clear old leases or widen the pool if the scope is exhausted


---

## 🔗 Full Lab Documentation

This scenario was fully documented in the DHCP Configuration Portfolio, including:

- ✅ Complete Packet Tracer lab setup
- ✅ Router DHCP configuration commands
- ✅ Fault simulation steps
- ✅ Step-by-step fix with CLI commands
- ✅ Verification screenshots
- ✅ Real-world help desk ticket

→ View the full lab here: [APIPA (169.254.x.x) Troubleshooting Lab](https://github.com/seemasm20-source/networking-labs/blob/main/02-dhcp-configuration/troubleshooting/apipa-issues.md)

---


💡 Next Step

→ Scenario 2 :[DHCP Pool Missing](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%202-ip%20addressing/dhcp-pool-missing.md)

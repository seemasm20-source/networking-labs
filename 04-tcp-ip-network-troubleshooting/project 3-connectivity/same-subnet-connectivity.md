
# 🔴 Connectivity 3 - Same Subnet Cannot Communicate

[ Back to Project README] → [README.md](./README.md)

---

## 📋 Problem Summary

  Two PCs on the same network cannot reach each other. Ping between them fails, even though both PCs have valid IP addresses and can reach the gateway and the internet individually.

---


## 💡 What Blocks Communication Inside a Subnet?

  When both PCs work normally with the gateway, the network, cable and switch are usually fine. The most likely cause is that the receiving PC drops the incoming ping. By default, Windows    Defender Firewall blocks inbound ICMP echo requests on some network profiles.

| Possible cause | Notes |
|----------------|-------|
| Windows Firewall blocking ICMP (ping) | Most likely, because the gateway ping works |
| Wrong subnet mask on one PC | Possible cause in general; not checked in this lab |
| Switch or cable fault | Unlikely, because both PCs reach the gateway |

> **First check:** if both PCs can ping the gateway but not each other, suspect the firewall on the receiving PC.

---


## 🔎 Verify the Problem 

| Test | Command | Result | Meaning |
|------|---------|--------|---------|
| 1. Ping PC2 from PC1 | `ping 192.168.10.11` | Request timed out ❌ | PC2 does not answer PC1 |
| 2. Ping the gateway from PC1 | `ping 192.168.10.1` | Reply ✅ | PC1's network connection works |

```text
C:\> ping 192.168.10.11
Request timed out.

C:\> ping 192.168.10.1
Reply from 192.168.10.1: bytes=32 time<1ms TTL=64
```



The network path works, but PC2 does not answer ping, which points to the firewall on PC2 as a likely cause. This is a lead to test, not a confirmed diagnosis until the fix works.

---



## 🔧 Fix

  On **PC2** (the PC that receives the ping), allow inbound ICMP echo requests:

**Control Panel → Windows Defender Firewall → Advanced settings → Inbound Rules**

Enable the rule **File and Printer Sharing (Echo Request - ICMPv4-In)**.

> Enable the rule on the profile in use (Private, Domain or Public). On a shared or public network, set the rule's scope to the local subnet only.

---



## 📝 Technical Note

A failed ping between two PCs does **not** automatically mean that a firewall is blocking ICMP traffic. Checking the firewall is one **troubleshooting step**, not a guaranteed **solution**.

The same symptom can result from several other causes:

- **Firewall rules and security policies:** Windows Firewall, third-party firewalls, endpoint security software or Group Policy may block ICMP traffic.
- **VLAN or switch issues:** The PCs may be connected to different VLANs, or a switch port may be misconfigured or faulty.
- **IP configuration issues:** Incorrect subnet masks, duplicate IP addresses or incorrect IP configurations can prevent communication.
- **SMB permissions:** If ping works but file or printer sharing fails, investigate SMB firewall rules, sharing permissions and NTFS permissions rather than ICMP connectivity.

**Recommended troubleshooting approach:** Confirm the connectivity issue using ping, check the receiving PC's firewall rules, verify IP configuration, and investigate VLAN, switch and security policies if necessary.

Change one setting at a time and retest after each change to identify the actual root cause.

---


## 💡 Next Step

→ Project 4 [Network Services](https://github.com/seemasm20-source/networking-labs/tree/main/04-tcp-ip-network-troubleshooting/project%204-network%20services)

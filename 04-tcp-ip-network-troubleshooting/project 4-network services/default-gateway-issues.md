
# 🔴 Service 2 - Default Gateway Issues

[ Back to Project README] → [README.md](./README.md)

---

## 📋 Problem Summary

A PC can communicate on its local network but cannot reach the internet or other network segments. In this lab the cause was an incorrect default gateway configured on the PC.

---

## 💡 What is a Default Gateway Issue?

The default gateway is the router address a PC uses to leave its local network. If the gateway setting is wrong, or the gateway itself is unavailable, local traffic still works but anything outside the subnet fails.

| Possible cause | Notes |
|----------------|-------|
| Wrong gateway IP configured | The cause in this lab |
| Router interface down | Gateway address is correct but does not reply |
| Gateway device offline | The router is powered off or unreachable |
| Gateway IP changed after router replacement | PCs with static settings still use the old address |

> **First check:** compare the gateway shown by `ipconfig` with the correct router address.

---

## 🔎 Verify the Problem

| Test | Command | Result | Meaning |
|------|---------|--------|---------|
| 1. Check the gateway setting | `ipconfig` | Default Gateway `192.168.0.250` ❌ | The gateway differs from the correct router address (`192.168.0.1`) |
| 2. Ping the configured gateway | `ping 192.168.0.250` | Request timed out ❌ | No device answers at this address |

```text
C:\> ipconfig
Default Gateway . . . . . : 192.168.0.250     ← incorrect

C:\> ping 192.168.0.250
Request timed out.
```

**Screenshot: incorrect gateway and failed ping:**

<img width="1920" height="1080" alt="ipconfig showing the gateway 192.168.0.250 and a failed ping" src="https://github.com/user-attachments/assets/e92a6318-5a31-4339-9f26-c0d849289724" />

---

## 🔧 Fix

Set the IPv4 configuration from **Manual** back to **Automatic (DHCP)**, so the PC receives the correct gateway:

**Settings → Network & internet → Wi-Fi → Hardware properties → IP assignment → Edit → Automatic (DHCP)**

If the PC needs a static address, enter the correct default gateway (`192.168.0.1`) instead.

> If the gateway address is correct but still does not reply, the fault is on the router side (interface down or device offline), not in the PC settings.

---

## ✅ Verification

```text
C:\> ping 192.168.0.1
C:\> tracert 8.8.8.8
C:\> ping 8.8.8.8
```

| Command | Result | Meaning |
|---------|--------|---------|
| `ping 192.168.0.1` | Reply ✅ | The gateway is reachable |
| `tracert 8.8.8.8` | First hop `192.168.0.1` ✅ | Traffic leaves through the gateway |
| `ping 8.8.8.8` | Reply ✅ | Internet connectivity is restored |

**Screenshot: gateway reachable and internet restored:**

<img width="1920" height="1080" alt="Successful ping to the gateway, tracert via the gateway and ping to 8.8.8.8" src="https://github.com/user-attachments/assets/0168d80b-f632-481f-8872-92a84ae85180" />

---

## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | PC cannot reach the internet or other network segments |
| **Cause** | Incorrect default gateway (`192.168.0.250` instead of `192.168.0.1`) |
| **Symptom** | Local network works; gateway ping times out; no access outside the subnet |
| **Diagnose** | `ipconfig` showed the wrong gateway; `ping 192.168.0.250` timed out |
| **Fix** | Set the IPv4 configuration back to Automatic (DHCP) |
| **Verified** | Gateway ping, `tracert` first hop and `ping 8.8.8.8` all succeeded |

---

## 🔗 Related Lab

→ [Cannot Reach Default Gateway](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%203-connectivity/cannot-ping-gateway.md)












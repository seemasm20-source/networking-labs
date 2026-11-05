




# 🔴 Service 3 - Port Blocked Scenarios

[ Back to Project README] → [README.md](./README.md)

---



## 📋 Problem Summary

A user can ping a server but cannot connect to a specific service. The application fails even though the server is reachable. In this example the user cannot connect with Remote Desktop (RDP) because port 3389 is blocked.

---

## 💡 What is a Blocked Port?

Ping uses ICMP and has no port number. Applications use ports, so a firewall can allow ping while blocking the port a service needs.

| Symptom | Detail |
|---------|--------|
| Ping to the server works | The network path and the server are reachable |
| One service fails | The application port is blocked or the service is unavailable |

> **First check:** if ping works but one application fails, test the application's port.

### Common Ports

| Port | Transport | Service | Used for |
|------|-----------|---------|----------|
| 80 | TCP | HTTP | Websites (unencrypted) |
| 443 | TCP | HTTPS | Websites (encrypted) |
| 53 | UDP and TCP | DNS | Name resolution |
| 3389 | TCP | RDP | Windows Remote Desktop |
| 445 | TCP | SMB | Windows file sharing |
| 9100 | TCP | RAW / JetDirect | Network printing |
| 22 | TCP | SSH | Secure remote access |
| 25 | TCP | SMTP | Email sending |

---

## 📝 Technical Note

A failed connection does **not** prove that the port is blocked by a firewall. Testing the port is a troubleshooting step. The same symptom can come from:

- Remote Desktop not enabled on the server
- The service not running, or nothing listening on the port
- The user not being allowed to connect (not in the **Remote Desktop Users** group)
- A firewall rule on the server, a network firewall or Group Policy

It becomes the confirmed cause only when the fix restores the connection.

---

## 🔎 Verify the Problem

| Test | Command | Result | Meaning |
|------|---------|--------|---------|
| 1. Check connectivity | `ping server` | Reply ✅ | IP connectivity works |
| 2. Test the RDP port | `Test-NetConnection server -Port 3389` | `TcpTestSucceeded : False` ❌ | Nothing accepts connections on port 3389 |

```text
PS C:\> Test-NetConnection server -Port 3389

TcpTestSucceeded : False
```

The server replies to ping but does not accept connections on port 3389, so the inbound RDP rule or the Remote Desktop setting is the likely cause.

---

## 🔧 Fix

On the **server** (the PC being connected to), check both settings:

**1. Enable Remote Desktop:**

**Settings → System → Remote Desktop → Enable Remote Desktop**

**2. Enable the firewall rule:**

**Windows Defender Firewall → Advanced settings → Inbound Rules**

Enable **Remote Desktop - User Mode (TCP-In)** for the profile in use.

> Windows Home editions cannot host Remote Desktop connections. Do not open port 3389 directly to the internet. Use a VPN instead.

---

## ✅ Verification

```text
PS C:\> Test-NetConnection server -Port 3389

TcpTestSucceeded : True
```

| Check | Result | Meaning |
|-------|--------|---------|
| `Test-NetConnection server -Port 3389` | `TcpTestSucceeded : True` ✅ | The port accepts connections |
| Connect with **Remote Desktop Connection** (`mstsc`) | Session opens ✅ | The user can use the service |

---

## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | User can ping a server but cannot connect with RDP |
| **Cause** | Port 3389 blocked by the inbound firewall rule or Remote Desktop disabled on the server |
| **Symptom** | Ping works; the RDP connection fails |
| **Diagnose** | `ping` succeeded; `Test-NetConnection -Port 3389` failed |
| **Fix** | Enabled Remote Desktop and the **Remote Desktop - User Mode (TCP-In)** rule on the server |
| **Verified** | Port test succeeded and the RDP session opened |

---

## 💡 Next Step

→ [Project 5][Ping & Tracert Troubleshooting](https://github.com/seemasm20-source/networking-labs/tree/main/04-tcp-ip-network-troubleshooting/project%205-ping%26tracert.md)








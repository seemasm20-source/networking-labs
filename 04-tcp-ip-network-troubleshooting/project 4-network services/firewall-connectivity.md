

# 🔴 Service 4 - Firewall Connectivity Issues (User Cannot Access Shared Drive)

[ Back to Project README] → [TCP/IP Network Troubleshooting - README.md](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/README.md)

---

## 📋 Problem Summary

A user can ping the file server, but cannot open a shared folder on it. The issue appeared after a Windows update or a security policy change.

---

## 💡 What is a Firewall Service Block?

Ping uses ICMP, while file sharing uses SMB on TCP port 445. A firewall can allow one and block the other, so a server can reply to ping while a specific application cannot connect.

| Symptom | Detail |
|---------|--------|
| Ping to the server works | The network path and the server are reachable |
| The shared folder does not open | The application port is blocked or the service is unavailable |
| Started after an update or policy change | Updates and policies can reset or change firewall rules |

> **First check:** if ping works but one application fails, suspect a firewall rule or the service itself, not the network.

---

## 📝 Technical Note

"System error 53" means the network path was not found. A blocked SMB port is a likely cause here, but it is not the only one. The same error can also come from:

- The file sharing service not running on the server
- A wrong server name or share name
- Name resolution problems
- Other firewall rules, third-party security software or Group Policy

Checking the firewall is a troubleshooting step. It becomes the confirmed cause only when enabling the rule restores access.

---

## 🔎 Verify the Problem

| Test | Command | Result | Meaning |
|------|---------|--------|---------|
| 1. Check network connectivity | `ping FILESERVER01` | Reply ✅ | The server is reachable |
| 2. Access the shared folder | `net use \\192.168.10.20\share` | System error 53: network path not found | File sharing (SMB, port 445) is likely blocked |

```text
C:\> ping FILESERVER01
Reply from 192.168.10.20

C:\> net use \\192.168.10.20\share
System error 53 has occurred.
The network path was not found.
```

The server answers ping, but the shared folder cannot be reached, so the inbound file sharing rule is the likely cause.

---

## 🔧 Fix

On the **file server**, enable the inbound SMB rule:

**Control Panel → Windows Defender Firewall → Advanced settings → Inbound Rules**

Right-click **File and Printer Sharing (SMB-In)** for the **Private** profile, then select **Enable Rule** ✅

> Enable the rule only on the profile in use. Do not enable it on the Public profile, and limit its scope to the local subnet where possible.

**Screenshot: SMB inbound rule enabled:**

<img width="1920" height="1080" alt="Windows Defender Firewall inbound rule File and Printer Sharing (SMB-In) enabled" src="https://github.com/user-attachments/assets/e7d59b2f-42d2-48d7-8a46-87a4e94734fd" />

---

## ✅ Verification

```text
C:\> net use \\192.168.10.20\share
The command completed successfully.
```

| Check | Result | Meaning |
|-------|--------|---------|
| `net use \\192.168.10.20\share` | Command completed successfully ✅ | The connection to the share works |
| Open `\\192.168.10.20\share` in File Explorer | Folder opens ✅ | The user can access the shared folder |

Enabling the rule restored access, which confirms the blocked SMB rule was the cause in this lab.

---

## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | User cannot access a shared folder on the file server |
| **Cause** | The inbound File and Printer Sharing (SMB-In) rule was disabled, blocking port 445 |
| **Symptom** | Ping works; `net use` fails with system error 53 |
| **Diagnose** | Ping succeeded, but `net use \\192.168.10.20\share` failed |
| **Fix** | Enabled the File and Printer Sharing (SMB-In) inbound rule for the Private profile |
| **Verified** | `net use` completed successfully and the shared folder opened |

---

## 💡 Next Step

→ [Service 5](./service-5.md)






# 🔴 Project 2: DNS Troubleshooting Lab

[← Back to DNS Portfolio README](../README.md)

---

## 📋 Overview

Five real-world DNS fault scenarios, each built and tested on Windows 11. Every scenario follows the same structure: problem, cause, verify, fix, verification and issue summary.

---

## 🏗️ Environment

| Component | Detail |
|-----------|--------|
| **Operating System** | Windows 11 |
| **Network Type** | Home network |
| **Tools** | Command Prompt, Windows network settings, Chrome / Edge |

---

## 📁 Scenarios

| # | Scenario | Root Cause | File |
|---|----------|------------|------|
| 1 | Ping by IP works, name fails | Missing or incorrect A record | [Missing A Record](./missing-a-record.md) |
| 2 | Cannot open any website (only one user affected) | Wrong DNS server configured on the PC | [Wrong DNS Server](./wrong-dns-server.md) |
| 3 | Intranet website not loading | Incorrect internal or external DNS configuration | [Internal vs External DNS](./internal-vs-external-dns.md) |
| 4 | New server unreachable by name | Hostname not added to DNS | [Hostname Not Resolving](./hostname-not-resolving.md) |
| 5 | Cannot open any website (entire office) | DNS service down | [DNS Service Down](./dns-service-down.md) |

---

## 📋 Reference

→ [DNS Cheatsheet](../project-4-nslookup/dns-cheatsheet.md)

---

## 💡 Next Step

→ [Project 3: DNS Cache Troubleshooting](../project-3-cache/)

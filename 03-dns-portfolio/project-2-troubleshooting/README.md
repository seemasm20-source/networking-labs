# 🔴 Project 2: DNS Troubleshooting Lab

[ Back to DNS Portfolio README] → [DNS Troubleshooting — GitHub README](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/README.md)

---

## 📋 Overview

Four real-world DNS fault scenarios and a command cheatsheet, built and tested on Windows 11. Each scenario follows the same structure: problem summary, cause, verify the problem, fix, verification and issue summary.

Scenario 2 was built and tested end to end on a real machine. Scenarios 1, 3 and 4 need an enterprise DNS server, so they show the troubleshooting method and are marked with a Lab Note.

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
| 3 | Intranet website not loading | Incorrect internal or external DNS configuration | [Internal Website Not Loading](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-2-troubleshooting/internal-vs-external.md) |
| 4 | Cannot open any website (entire office) | DNS service down | [DNS Service Down](./dns-service-down.md) |

---

## 📋 Reference

| File | Description |
|------|-------------|
| [DNS Cheatsheet](./dns-cheatsheet.md) | Command reference, troubleshooting decision flow and diagnostic checklist |

---

## 💡 Next Step

→ [Project 3: DNS Cache Troubleshooting](../project-3-cache/)

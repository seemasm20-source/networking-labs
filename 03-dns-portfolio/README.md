      ## Networking-labs / 03-dns-portfolio / README.md


# 🌐 DNS Troubleshooting Portfolio

**Portfolio:** IT Help Desk Tier 1 & Tier 2 - Networking Labs

**Tool:** Windows 11 (Command Prompt, network settings)

**Purpose:** Demonstrate hands-on DNS troubleshooting skills for IT Help Desk Tier 1 and Tier 2

**Author:** Seema Soapanahalli Mallikarjunaiah

**Date:** May 2026

---

## 📌 Objective

This project covers DNS from fundamentals to troubleshooting,
using real Windows 11 command-line tools and simulated
help desk scenarios.

The objective of this project is to demonstrate:

- Understanding of what DNS is and how name resolution works
- Diagnosis of common DNS faults using `ping`, `nslookup`
  and `ipconfig`
- DNS cache troubleshooting using `ipconfig /displaydns`
  and `ipconfig /flushdns`
- Forward and reverse lookups using `nslookup`
- Clear escalation of faults that are outside Tier 1 & 2 scope

> **Lab Note:** An enterprise DNS server outage cannot be
> reproduced in a home lab. Where a scenario depends on a
> company DNS server, the client-side commands show the standard
> troubleshooting method and the expected results are labelled
> as such. Commands that can be run on a real machine, such as
> public-DNS tests, cache commands and `nslookup`, were run on
> Windows 11. Internal DNS addresses used in the scenarios are
> fictional.

---

## 💡 What is DNS?

DNS (Domain Name System) is a network service that translates
human-readable hostnames, such as `google.com`, into IP addresses,
so devices can find each other on a network.

Without DNS, users would need to remember the IP address of
every website and server they want to reach.

| Without DNS | With DNS |
|-------------|----------|
| Users type IP addresses | Users type easy-to-remember names |
| Hard to remember and error-prone | Names stay the same even if the IP changes |
| Every change needs to be communicated | Changes are made once on the DNS server |

---

## 🔄 How DNS Resolution Works

When a user opens a website, the PC resolves the name in the
following order:

### 1. Check the local cache

Windows checks its DNS Resolver Cache for a stored answer.

### 2. Ask the configured DNS server

If there is no cached answer, the PC sends a query to the DNS
server set in its network settings.

### 3. DNS server finds the answer

The DNS server returns the answer from its own records or cache,
or looks it up on behalf of the PC.

### 4. Answer returned and cached

The PC receives the IP address, stores it in the cache and
connects to the destination.

```text
PC  ──Is it in my cache?──►  Local DNS cache
PC  ──Query: google.com───►  DNS Server
PC  ◄────IP address───────   DNS Server
PC  ──────Connects────────►  google.com
```

---

## 🔧 Tools Used

| Tool | Command | Purpose |
|------|---------|---------|
| Command Prompt | `ipconfig /all` | Shows the DNS server configured on the PC |
| nslookup | `nslookup hostname` | Tests DNS name resolution |
| nslookup | `nslookup hostname 8.8.8.8` | Queries a specific DNS server |
| ping | `ping hostname` | Tests name resolution and connectivity |
| ping | `ping 8.8.8.8` | Tests connectivity without DNS |
| ipconfig | `ipconfig /displaydns` | Shows the current DNS cache |
| ipconfig | `ipconfig /flushdns` | Clears all DNS cache entries |

---

## 📁 Portfolio Structure

| Project | Topic | Key Skills |
|---------|-------|------------|
| Project 1 | DNS Fundamentals | What DNS is, how it works, key terms |
| Project 2 | DNS Troubleshooting Lab | 5 real-world DNS fault scenarios, DNS cheatsheet |
| Project 3 | DNS Cache Troubleshooting | `displaydns`, `flushdns` |
| Project 4 | NSLOOKUP Lab | Forward and reverse lookup |

---

## 🔴 DNS Troubleshooting Scenarios

Five common DNS faults were diagnosed in Project 2, and two
more were covered in Project 3 (cache) and Project 4
(lookups). Full details are in each project folder.

| Scenario | Root Cause | Fix | Project |
|----------|------------|-----|---------|
| Cannot open any website | DNS service down | Isolated with `nslookup google.com 8.8.8.8`, escalated to Tier 2 / Infrastructure | [Project 2](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-2-troubleshooting/README.md) |
| New server unreachable by name | Hostname not resolving | Confirmed ping by IP works and name fails, requested DNS record check | [Project 2](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-2-troubleshooting/README.md) |
| Intranet website not loading | Incorrect internal or external DNS configuration | Corrected the DNS server setting on the PC | [Project 2](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-2-troubleshooting/README.md) |
| Ping by IP works, name fails | Missing or incorrect A record | Verified with `nslookup`, escalated for A record correction | [Project 2](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-2-troubleshooting/README.md) |
| Some websites work, some don't | Incorrect DNS server configuration | Corrected the DNS server on the PC | [Project 2](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-2-troubleshooting/README.md) |
| User sees an old version of a website | Stale DNS cache | `ipconfig /flushdns` | [Flush DNS](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-3-cache/flushdns.md) |
| DNS changes not reflected after server migration | Outdated DNS cache | `ipconfig /flushdns` | [Flush DNS](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-3-cache/flushdns.md) |
| Cannot access `fileserver.company.local` by hostname | Missing or incorrect A record (forward lookup failure) | Verified with `nslookup hostname` | [Project 4](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-4-nslookup/) |
| Unable to identify the hostname of an IP address | Missing or incorrect PTR record (reverse lookup failure) | Verified with `nslookup IP address` | [Project 4](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-4-nslookup/) |

---

## 📂 Project Files

| Section | Description | File |
|---------|-------------|------|
| Project 1 | DNS fundamentals: what DNS is, how it works, key terms | [DNS Fundamentals](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-1-fundamentals/) |
| Project 2 | 5 DNS fault scenarios and DNS cheatsheet | [DNS Troubleshooting Lab](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-2-troubleshooting/README.md) |
| Project 3 | `displaydns` and `flushdns` | [Flush DNS](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-3-cache/flushdns.md) |
| Project 4 | Forward and reverse lookup with `nslookup` | [NSLOOKUP Lab](https://github.com/seemasm20-source/networking-labs/blob/main/03-dns-portfolio/project-4-nslookup/) |

---

## 📚 Skills Demonstrated

- Explaining DNS and the name resolution process
- Using `nslookup` to test name resolution and query a specific DNS server
- Separating DNS faults from network faults with `ping` by IP and by name
- Isolating a company DNS fault by querying a public DNS server
- Clearing stale entries with `ipconfig /flushdns`
- Forward lookups (A and AAAA records) and reverse lookups (PTR records)
- Deciding when to fix a fault at Tier 1 & 2 and when to escalate
- Technical documentation for a GitHub portfolio

---

## 🎯 Real-World Help Desk Tickets

| Caller Complaint | Root Cause | Fix Applied |
|------------------|------------|-------------|
| "I can't open any website" | DNS service down | Isolated with `nslookup google.com 8.8.8.8`, escalated to Tier 2 |
| "I can reach the server by IP but not by name" | Missing or incorrect A record | Confirmed with `nslookup`, escalated for correction |
| "The intranet site won't load" | Incorrect DNS configuration | Corrected the DNS server setting |
| "Some websites work and some don't" | Incorrect DNS server configuration | Corrected the DNS server on the PC |
| "I still see the old version of the website" | Stale DNS cache | `ipconfig /flushdns` |

---

## 🎓 Learning Outcome

This project provided hands-on experience diagnosing DNS faults
on Windows 11 using built-in command-line tools.

It built practical understanding of how to tell a DNS fault from
a network fault, how to test name resolution, and when a fault
needs to be escalated, which is directly relevant to IT Help
Desk Tier 1 & 2 roles.

---

## ✅ Conclusion

Across four projects, common DNS faults were identified,
diagnosed and resolved or escalated:

- DNS service down
- Hostname not resolving
- Incorrect DNS server configuration
- Missing or incorrect A and PTR records


Together these show a systematic approach to fault isolation:
confirm the symptom, test by IP and by name, isolate the DNS
server, fix what Tier 1 & 2 can fix and escalate the rest.

## networking-labs / 04-tcp-ip-network-troubleshooting / README.md

# 🌐 TCP/IP Network Troubleshooting Portfolio

**Portfolio:** IT Help Desk Tier 1 & Tier 2 - Networking Labs

**Tool:** Windows 10/11 (Command Prompt, network settings, Windows Defender Firewall)

**Purpose:** Demonstrate hands-on TCP/IP troubleshooting skills for IT Help Desk Tier 1 and Tier 2

**Author:** Seema Soapanahalli Mallikarjunaiah

**Date:** April 2026

---

## 📌 Objective

This portfolio covers TCP/IP from fundamentals to real-world troubleshooting using Windows command-line tools and simulated help desk scenarios.

The objective of this portfolio is to demonstrate:

- Understanding of the TCP/IP model, IPv4 addressing and the default gateway
- Diagnosis of IP addressing faults: APIPA, missing or exhausted DHCP pools and IP address conflicts
- Diagnosis of connectivity faults: wrong gateway, DNS failures, blocked ping and intermittent drops
- Diagnosis of service faults: blocked ports, firewall rules and shared drive access
- Use of `ping`, `tracert`, `pathping`, `nslookup`, `arp`, `netstat` and `ipconfig` to find where a fault starts
- A step-by-step method for "no internet" and "slow network" complaints

> **Lab Note:** Faults that come and go, such as intermittent drops and slow performance, cannot be reproduced on demand. Where a scenario uses illustrative output, it is labelled as such. Commands that were run on a real machine have screenshots.

---

## 💡 What is TCP/IP?

TCP/IP is the set of protocols that devices use to communicate on a network, including the internet. **TCP** delivers data reliably and in order. **IP** handles addressing and routing between devices.

| Layer | Name | Examples |
|:-----:|------|----------|
| 4 | **Application** | HTTP, HTTPS, DNS, FTP, SMTP, RDP |
| 3 | **Transport** | TCP, UDP |
| 2 | **Internet** | IPv4, IPv6, ICMP (ping) |
| 1 | **Network Access** | Ethernet, Wi-Fi, MAC addresses, switches |

Every device needs three core settings: an **IP address**, a **subnet mask** and a **default gateway**. Most also need a **DNS server** to use names.

---

## 🎯 Troubleshooting Approach

Work from the PC outward. The first test that fails shows where the problem is.

| Step | Command | Tests |
|:----:|---------|-------|
| 1 | `ipconfig /all` | IP address, mask, gateway, DNS and DHCP settings |
| 2 | `ping <own IP>` | The adapter's IP configuration |
| 3 | `ping <default gateway>` | The local network |
| 4 | `ping 8.8.8.8` | Routing to the internet |
| 5 | `ping google.com` | DNS name resolution |

If these pass but one application fails, test the application's port, and check the firewall and the service itself.

---

## 🔧 Tools Used

| Tool | Purpose |
|------|---------|
| `ipconfig` | Shows and refreshes the IP configuration and the DNS cache |
| `ping` | Tests connectivity and measures delay and packet loss |
| `tracert` | Shows each router between the PC and the destination |
| `pathping` | Combines ping and tracert, with packet loss per hop |
| `nslookup` | Tests DNS name resolution |
| `arp -a` | Shows the IP-to-MAC table, useful for duplicate IPs |
| `netstat -an` | Shows connections and listening ports |
| `route print` | Shows the routing table |
| Windows Defender Firewall | Checks inbound rules for ICMP, SMB and RDP |

---

## 📁 Portfolio Structure

| Project | Topic | Key Skills |
|---------|-------|------------|
| Project 1 | TCP/IP Fundamentals | TCP/IP model, IPv4, public and private IPs, default gateway |
| Project 2 | IP Addressing Troubleshooting | APIPA, DHCP pool missing and exhausted, IP address conflict |
| Project 3 | Connectivity Troubleshooting | Gateway, DNS, blocked ping, intermittent connectivity |
| Project 4 | Network Services Troubleshooting | Default gateway, blocked ports, firewall and shared drives |
| Project 5 | Ping and Tracert Lab | Ping and tracert guides, reading results |
| Project 6 | Real-World Scenarios | No internet investigation, slow network performance |

---

## 🔴 TCP/IP Troubleshooting Scenarios

| Scenario | Root Cause | Fix | Topic |
|----------|------------|-----|-------|
| PC shows 169.254.x.x | APIPA: the PC could not reach a DHCP server | `ipconfig /release` and `/renew`; DHCP service or pool restored | [APIPA Troubleshooting](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%202-ip%20addressing/apipa-issues.md) |
| New PC gets no IP address | DHCP pool missing | Recreated the DHCP pool | [DHCP Pool Missing](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%202-ip%20addressing/dhcp-pool-missing.md) |
| Connection drops, IP conflict warning | Duplicate IP address | Set one device to DHCP or a unique IP | [Duplicate IP](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%202-ip%20addressing/duplicate-ip.md) |
| Cannot ping gateway | Wrong default gateway configured manually | Set back to Automatic (DHCP) | [Cannot Ping Default Gateway – Troubleshooting](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%203-connectivity/cannot-ping-gateway.md) |
| Ping by IP works, name fails | DNS server wrong or unreachable | Set a valid DNS server | [Ping IP Works, Name Fails](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%203-connectivity/ping-ip-works-name-fails.md) |
| Same-LAN PC unreachable | Firewall blocking ICMP (other causes possible) | Enabled the inbound ICMP echo rule | [Same Subnet Connectivity Issues](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%203-connectivity/same-subnet-connectivity.md/) |
| Internet randomly drops | Weak Wi-Fi, cable or ISP packet loss | Improved Wi-Fi, replaced the cable, contacted the ISP | [Intermittent Connectivity](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%203-connectivity/intermittent-connectivity.md) |
| Gateway unreachable, no internet | Incorrect default gateway | Set back to Automatic (DHCP) | [Default Gateway Issues – Troubleshooting](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%204-network%20services/default-gateway-issues.md) |
| Cannot RDP to server | Port 3389 blocked or Remote Desktop disabled | Enabled Remote Desktop and the inbound rule | [Port Blocked Scenarios](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%204-network%20services/port-blocked-scenarios.md) |
| No internet at all | Depends on the first failing test | Fixed the failing layer | [No Internet Connectivity – Troubleshooting Flowchart](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%206-real%20world%20tickets/no-internet-flowchart.md) |
| Slow internet | Packet loss or delay, local or ISP | Found the cause with `ping -t` and `pathping` | [Slow Network Performance – Troubleshooting Ticket](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%206-real%20world%20tickets/slow-network-performance.md/) |


---

## 📂 Project Files

| Section | Description | File |
|---------|-------------|------|
| Project 1 | TCP/IP fundamentals | [TCP/IP Fundamentals](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%201-fundamentals/tcp-ip-fundamentals.md) |
| Project 2 | APIPA, pool missing, pool exhaustion, IP conflict | [IP Addressing – Troubleshooting Projects](https://github.com/seemasm20-source/networking-labs/tree/main/04-tcp-ip-network-troubleshooting/project%202-ip%20addressing/) |
| Project 3 | Gateway, DNS, blocked ping, intermittent connectivity | [[Network Connectivity Troubleshooting Projects](https://github.com/seemasm20-source/networking-labs/tree/main/04-tcp-ip-network-troubleshooting/project%203-connectivity/) |
| Project 4 | Default gateway, blocked ports, firewall | [[Network Services – Troubleshooting Projects](https://github.com/seemasm20-source/networking-labs/tree/main/04-tcp-ip-network-troubleshooting/project%204-network%20services/) |
| Project 5 | Ping Guide and Tracert Guide | [Ping and Tracert Lab](./project-5-ping-tracert/) |
| Project 6 | No internet and slow network | [Real-World Scenarios](./project-7-real-world-scenarios/) |

---

## 📚 Skills Demonstrated

- Explaining the TCP/IP model, IPv4 addressing and the default gateway
- Diagnosing APIPA, DHCP pool and IP conflict faults
- Testing from the PC outward: configuration, own IP, gateway, internet, DNS
- Using `ping`, `tracert` and `pathping` to find where delay or loss starts
- Telling a DNS fault from a network fault
- Checking firewall rules and ports for blocked services, while recognising that a firewall is one possible cause and not the only one
- Reading `ipconfig`, `nslookup`, `tracert` and `ping` output
- Technical documentation for a GitHub portfolio

---

## 🎯 Real-World Help Desk Tickets

| Caller Complaint | Root Cause | Fix Applied |
|------------------|------------|-------------|
| "I have no internet" | First failing test in the 5-step method | Fixed the failing layer |
| "My PC says limited connectivity" (169.254.x.x) | PC could not reach a DHCP server | `ipconfig /release` and `/renew`, DHCP restored |
| "I can open IPs but not websites" | DNS server wrong or unreachable | Set a valid DNS server |
| "I can't reach my colleague's PC" | Firewall blocking ICMP | Enabled the inbound echo rule |
| "My connection keeps dropping" | Packet loss from Wi-Fi, cable or ISP | Improved Wi-Fi, replaced the cable, contacted the ISP |
| "I can't connect to the server with Remote Desktop" | Port 3389 blocked | Enabled Remote Desktop and the inbound rule |
| "I can't open the shared folder" | Port 445 blocked | Enabled the SMB inbound rule |

---

## 🎓 Learning Outcome

This portfolio provided hands-on experience diagnosing TCP/IP faults on Windows using built-in command-line tools.

It built practical understanding of how to test from the PC outward, how to separate IP, gateway, DNS and firewall faults, and how to read ping, tracert and nslookup output, which is directly relevant to IT Help Desk Tier 1 and Tier 2 roles.

---

## ✅ Conclusion

Across seven projects, common TCP/IP faults were identified, diagnosed and resolved:

- APIPA and DHCP pool faults
- IP address conflicts
- Wrong default gateway
- DNS name resolution failures
- Firewall and blocked-port problems
- Packet loss and slow performance

Together these show a systematic approach to fault isolation: confirm the symptom, test from the PC outward, find the failing layer, fix it and verify.

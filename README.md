
# 🌐 LAN-to-LAN Routing Using Cisco Router


**Portfolio:** IT Help Desk Tier 1 & Tier 2 - Networking Labs

**Tool:** Cisco Packet Tracer
  
**Purpose:** Network simulation and troubleshooting practice

**Author:** Seema Soapanahalli Mallikarjunaiah

**Date:** May 2026

---

## 📌 Objective

This project simulates two office departments 
**HR (LAN 1)** and **Finance (LAN 2)**  operating
on separate networks within the same organisation.

A Cisco 2911 router connects both departments and
enables communication between them while maintaining
network segmentation.

**Networking concepts covered:**
- LAN segmentation and IPv4 addressing
- Router interface configuration via Cisco CLI
- Default gateway setup and troubleshooting
- Inter-LAN connectivity testing
- Network fault diagnosis and resolution

---






## 🚀 How to install Cisco Packet Tracer

1. Visit the official Cisco Networking Academy Resource Hub. [Cisco Networking Academy Resource Hub](https://www.netacad.com/resources/lab-downloads)

2. Sign in to your Cisco account.

3. Download the Windows version of Cisco Packet Tracer.

4. Open the downloaded installer and follow the installation wizard.

5. After installation, launch Cisco Packet Tracer from the Windows Start menu.









## 🖥️ Network Topology

```
                    ROUTER (Cisco 2911)
                   /                   \
          Gi0/0                         Gi0/1
    IP: 10.0.0.4                  IP: 192.168.1.4
           |                             |
    SWITCH 1 (2960)              SWITCH 2 (2960)
   /      |      \              /      |      \
 PC1     PC2     PC3          PC1     PC2     PC3

 ◄────── LAN 1 (HR) ────────► ◄──── LAN 2 (Finance) ────►
  Network: 10.0.0.0/24          Network: 192.168.1.0/24
  Gateway: 10.0.0.4             Gateway: 192.168.1.4
```

---

## 📋 Network Addressing Plan

### LAN 1 - HR Department

| Device       | IP Address | Subnet Mask   | Gateway  |
|--------------|------------|---------------|----------|
| Router Gi0/0 | 10.0.0.4   | 255.255.255.0 | —        |
| PC1          | 10.0.0.1   | 255.255.255.0 | 10.0.0.4 |
| PC2          | 10.0.0.2   | 255.255.255.0 | 10.0.0.4 |
| PC3          | 10.0.0.3   | 255.255.255.0 | 10.0.0.4 |

### LAN 2 - Finance Department

| Device       | IP Address  | Subnet Mask   | Gateway     |
|--------------|-------------|---------------|-------------|
| Router Gi0/1 | 192.168.1.4 | 255.255.255.0 | —           |
| PC1          | 192.168.1.1 | 255.255.255.0 | 192.168.1.4 |
| PC2          | 192.168.1.2 | 255.255.255.0 | 192.168.1.4 |
| PC3          | 192.168.1.3 | 255.255.255.0 | 192.168.1.4 |

---

## 🔧 Devices Used

| Device | Model      | Qty | Purpose                       |
|--------|------------|-----|-------------------------------|
| Router | Cisco 2911 | 1   | Routes traffic between 2 LANs |
| Switch | Cisco 2960 | 2   | Connects PCs within each LAN  |
| PC     | Generic PC | 6   | End users - 3 per department  |

---

## 🛠️ Technologies Used

| Technology          | Purpose                        |
|---------------------|--------------------------------|
| [Cisco Packet Tracer](https://www.netacad.com/resources/lab-downloads) | Network simulation tool |
| Cisco 2911 Router   | Inter-LAN routing via CLI      |
| Cisco 2960 Switch   | Layer 2 switching within LANs  |
| IPv4 Addressing     | Static IP on all devices       |
| Cisco IOS CLI       | Device configuration           |
| ICMP Ping           | Connectivity verification      |

---

## ✅ Connectivity Test Results

| Source     | Destination | Same LAN | Result   |
|------------|-------------|----------|----------|
| 10.0.0.1   | 10.0.0.2    | ✅ Yes   | Reply ✅ |
| 10.0.0.1   | 10.0.0.3    | ✅ Yes   | Reply ✅ |
| 10.0.0.1   | 192.168.1.1 | ❌ No    | Reply ✅ |
| 10.0.0.1   | 192.168.1.2 | ❌ No    | Reply ✅ |
| 10.0.0.1   | 192.168.1.3 | ❌ No    | Reply ✅ |

---

## 🔴 Issues Encountered
                                                                                                         

Real problems faced during this lab-full details
in the troubleshooting folder.



| Issue | Cause | Fix | File |
|---|---|---|---|
| PCs Could Not Communicate Across LANs | Wrong default gateway on PCs | Set the correct gateway on all PCs | [Wrong Default Gateway Issue](https://github.com/seemasm20-source/networking-labs/blob/main/lan-to-lan-routing%20/troubleshooting/wrong-gateway-issue.md) |
| Router Interface Administratively Down | The `shutdown` command manually disabled the GigabitEthernet0/0 interface. | Enter interface configuration mode and use `no shutdown`. |  [Router Interface Down Issue](https://github.com/seemasm20-source/networking-labs/blob/main/lan-to-lan-routing%20/troubleshooting/interface-down.issue.md)|
| Shutdown Had No Effect on Same-LAN Ping | Same-LAN traffic bypasses the router. | Test cross-LAN connectivity instead. | [Router Interface Down Issue](https://github.com/seemasm20-source/networking-labs/blob/main/lan-to-lan-routing%20/troubleshooting/interface-down.issue.md)|




## 📂 Project Files

| Folder                                                                                                                   | Contents                                  |
| ------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------- |
| [topology](https://github.com/seemasm20-source/networking-labs/blob/main/lan-to-lan-routing%20/topology%20/topology.md)  | Network diagram and IP address table      |
| [config](https://github.com/seemasm20-source/networking-labs/blob/main/lan-to-lan-routing%20/%20config/router-config.md) | Full router CLI commands with explanation |
| [troubleshooting](https://github.com/seemasm20-source/networking-labs/tree/main/lan-to-lan-routing%20/troubleshooting)   | Issues found and fixed during the lab     |
---

## 📚 Skills Demonstrated

- Cisco 2911 router configuration via CLI
- Cisco 2960 switch topology design
- Static IPv4 addressing across two /24 networks
- Inter-LAN routing using directly connected routes
- Interface troubleshooting - show ip interface brief
- Routing table verification - show ip route
- Default gateway concepts and troubleshooting
- Cisco CLI level navigation
- Network fault isolation and root cause analysis
- Technical documentation

---

## 🎯 Real-World Help Desk Relevance

| Caller complaint | Root cause | Fix |
|------------------|------------|-----|
| Can reach colleagues but not other dept | Missing default gateway | Add correct gateway on PC |
| Whole department lost access suddenly | Router interface down | no shutdown on correct interface |
| One PC has no network access | Wrong IP or missing gateway | Check all 3 fields in IP config |

---


## 🎓 Learning Outcome

This project provided hands-on experience
configuring inter-LAN communication using
Cisco routers and switches in a simulated
enterprise environment.

Working through real configuration errors
and resolving them independently strengthened
practical understanding of:

- IPv4 addressing and subnetting across
  multiple networks
- Cisco IOS CLI-interface configuration
  and troubleshooting commands
- Default gateway concepts and how
  misconfiguration affects connectivity
- Fault isolation-identifying root cause
  before applying a fix

These are core skills required in IT Help
Desk Tier 1 and IT Support roles where
users frequently report connectivity issues
that trace back to gateway or interface
configuration problems.




---

## ✅ Conclusion


This lab successfully demonstrated
inter-LAN routing between two separate
department networks using a Cisco 2911
router confirmed through end-to-end
ping tests from HR to Finance.

What made this lab valuable was not
just getting it to work but breaking
it deliberately and fixing it.

Three real issues were encountered,
diagnosed and resolved using Cisco CLI
diagnostic commands. Each one reflects
a fault type that appears regularly in
real IT support environments:

- A wrong gateway stops users reaching
  other departments-one of the most
  common Help Desk calls
- An interface left administratively down
  takes out an entire network segment
- Understanding why same-LAN traffic
  bypasses the router is fundamental
  to isolating where a fault actually lives






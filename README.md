
# 🌐 LAN-to-LAN Routing Using Cisco Router

**Portfolio:** IT Help Desk Tier 1 — Networking Labs

**Tool:** Cisco Packet Tracer

**Author:** Seema

**Date:** May 14, 2026

---

## 📌 Objective

This project simulates two office departments —
**HR (LAN 1)** and **Finance (LAN 2)** — operating
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

### LAN 1 — HR Department

| Device       | IP Address | Subnet Mask   | Gateway  |
|--------------|------------|---------------|----------|
| Router Gi0/0 | 10.0.0.4   | 255.255.255.0 | —        |
| PC1          | 10.0.0.1   | 255.255.255.0 | 10.0.0.4 |
| PC2          | 10.0.0.2   | 255.255.255.0 | 10.0.0.4 |
| PC3          | 10.0.0.3   | 255.255.255.0 | 10.0.0.4 |

### LAN 2 — Finance Department

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
| PC     | Generic PC | 6   | End users — 3 per department  |

---

## 🛠️ Technologies Used

| Technology          | Purpose                        |
|---------------------|--------------------------------|
| [Cisco Packet Tracer](https://www.netacad.com/courses/getting-started-cisco-packet-tracer) | Network simulation tool |
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
                                                                                                         

Real problems faced during this lab — full details
in the troubleshooting folder.

| # | Issue | Cause | Fix | File |
|---|-------|-------|-----|------|
| 1 | PCs could not communicate across LANs | Wrong default gateway on PCs | Set correct gateway on all PCs **View Solution:** [Wrong Default Gateway Troubleshooting](https://github.com/seemasm20-source/networking-labs/blob/main/lan-to-lan-routing/troubleshooting/wrong-default-gateway-troubleshooting.md)  
view


| 2 | Router interface administratively down | The shutdown command was typed on GigabitEthernet0/0 which manually disabled the interface.| Entered interface mode first then no shutdown [View](https://github.com/seemasm20-source/networking-labs/blob/main/lan-to-lan-routing/troubleshooting/interface-down-issue.md)
| 3 | Shutdown had no effect on same-LAN ping | Same-LAN traffic bypasses router | Tested cross-LAN ping instead | [View](https://github.com/seemasm20-source/networking-labs/blob/main/lan-to-lan-routing/troubleshooting/interface-down-issue.md)



---

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
- Interface troubleshooting — show ip interface brief
- Routing table verification — show ip route
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

This project provided hands-on experience configuring
LAN-to-LAN communication using Cisco devices in a
simulated enterprise environment.

It strengthened practical understanding of IP addressing,
router CLI configuration, default gateway concepts and
fault isolation — skills directly relevant to IT Help
Desk Tier 1 and IT Support roles.

---

## ✅ Conclusion

Communication between HR (LAN 1) and Finance (LAN 2)
was successfully established using a Cisco 2911 router.
All cross-LAN pings confirmed full connectivity.

Three real troubleshooting issues were identified,
diagnosed and resolved — demonstrating practical
networking and fault isolation skills required in
entry-level IT Support positions.





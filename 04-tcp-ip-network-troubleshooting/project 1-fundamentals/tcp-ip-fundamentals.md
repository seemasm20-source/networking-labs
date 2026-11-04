# 📖 TCP/IP Fundamentals

---

## 💡 What is TCP/IP?

**TCP/IP** is the set of protocols that devices use to communicate on a network, including the internet. It is built from two main protocols.

### TCP: Transmission Control Protocol

TCP is a **connection-oriented** protocol that delivers data reliably and in the correct order. If data is lost on the way, TCP detects it and retransmits it.

### IP: Internet Protocol

IP works at the **Internet layer** (called the Network layer in the OSI model) and is responsible for **addressing and routing** data packets between devices. Each device on a network uses an IP address, which allows data to be sent from a source device to the correct destination device. Addresses are assigned by an administrator or automatically by DHCP.

---

## 🔄 The TCP/IP 4-Layer Model

| Layer | Name | Purpose | Examples |
|:-----:|------|---------|----------|
| 4 | **Application** | Services the user interacts with | HTTP, HTTPS, DNS, FTP, SMTP, RDP |
| 3 | **Transport** | Delivery between applications | TCP (reliable), UDP (fast, no confirmation) |
| 2 | **Internet** | IP addressing and routing | IPv4, IPv6, ICMP (ping) |
| 1 | **Network Access** | Physical delivery on the local network | Ethernet cables, Wi-Fi, MAC addresses, switches |

---

## 🌐 IPv4 Basics

An IPv4 address is written as four numbers separated by dots:

```text
192.168.10.50
```

IPv4 uses **32 bits** to represent an address, split into four groups of 8 bits (octets). Each octet is a number from 0 to 255.

```text
8 + 8 + 8 + 8 = 32 bits
```

**Three core settings for every device:**

| Setting | Purpose |
|---------|---------|
| **IP Address** | Identity on the network |
| **Subnet Mask** | Defines which addresses are local and which are remote |
| **Default Gateway** | The exit door to other networks (needed to leave the local network) |

> Most devices also need a **DNS server** so they can use hostnames such as `google.com`.

---

## 🏠 Public vs Private IP

**Private addresses** are used inside an office or home:

| Range | Notes |
|-------|-------|
| `10.0.0.0` – `10.255.255.255` | Large networks |
| `172.16.0.0` – `172.31.255.255` | Medium networks |
| `192.168.0.0` – `192.168.255.255` | Most common in homes and small offices |

Private addresses are only unique inside one network. Different networks can use the same private address.

**Public addresses** are assigned by an ISP and are unique worldwide.

---

## ⚙️ Static vs DHCP

| Type | How Assigned | Used For |
|------|--------------|----------|
| **Static** | Manually by an admin | Servers, printers, routers |
| **DHCP** | Automatically from a DHCP server | PCs, laptops, phones |

---

## 🚪 Default Gateway

The default gateway is the router address that devices use to leave their local network.

```text
C:\> ipconfig

Default Gateway . . . . . : 192.168.10.1     ← your router
```

| Without a gateway | With a gateway |
|-------------------|----------------|
| Stuck on the local network only | Can reach the internet and other LANs |

**Quick test:**

```text
C:\> ping 192.168.10.1
```

| Result | Meaning |
|--------|---------|
| ✅ Reply | The gateway is reachable |
| ❌ Request timed out | Possible gateway or connection problem (cable, switch or firewall can also cause this) |

---

## 📋 Key Facts for Tier 1

| Item | Detail |
|------|--------|
| **Loopback** | `127.0.0.1`: always your own PC (the whole `127.0.0.0/8` range is loopback) |
| **APIPA** | `169.254.x.x`: the PC could not reach a DHCP server and gave itself an address |
| **Common private range** | `192.168.x.x` |
| **Subnet /24** | `255.255.255.0` |
| **`ping 127.0.0.1`** | Tests the local TCP/IP stack |
| **`ping 8.8.8.8`** | Tests internet connectivity without using DNS (if the network allows ping) |

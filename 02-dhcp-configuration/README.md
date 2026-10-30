## networking-labs / dhcp-configuration / README.md




# 🌐 DHCP Server Configuration using Cisco Router


**Portfolio:** IT Help Desk Tier 1 & Tier 2 - Networking Labs

**Tool:** Cisco Packet Tracer
  
**Purpose:** Demonstrate DHCP server setup and troubleshooting skills for IT Help Desk Tier 1 and Tier 2

**Author:** Seema Soapanahalli Mallikarjunaiah

**Date:** May 2026





 ## 📌 Objective

This project simulates a small enterprise network
with two departments:

- HR (LAN 1)
- Finance (LAN 2)

A Cisco 2911 router is configured as a DHCP server
to automatically provide IP addresses and network
settings to client devices in both LANs.

The objective of this project is to demonstrate:

- DHCP configuration on a Cisco router using two
  separate address pools, one per LAN
- Automatic assignment of IP address, subnet mask,
  default gateway and DNS server to client devices
- Diagnosis and resolution of common DHCP faults:
  APIPA addressing (169.254.x.x), pool exhaustion
  and IP address conflicts
---

## 💡 What is DHCP?

DHCP (Dynamic Host Configuration Protocol) is a network
protocol that automatically assigns IP addresses and
other network settings to devices, so they can connect
to the network without manual setup.

Without DHCP, administrators must manually configure
every device with:

- IP Address
- Subnet Mask
- Default Gateway
- DNS Server

DHCP automates this process, reducing configuration
errors and simplifying network management.

| Without DHCP | With DHCP |
|--------------|-----------|
| Manual IP configuration | Automatic IP assignment |
| Time-consuming setup | Fast deployment |
| Higher risk of errors such as duplicate IPs | Consistent and centralised management |
---

## 🔄 DHCP Process (DORA)

DHCP uses a four-step process known as **DORA**
(Discover, Offer, Request, Acknowledge):

### 1. Discover

The client broadcasts a request to locate a DHCP server.

### 2. Offer

The DHCP server responds with an available IP address.

### 3. Request

The client requests to use the offered IP address.

### 4. Acknowledge

The DHCP server confirms the lease and provides
network configuration details.

```
Client  ──Discover──►  DHCP Server
Client  ◄───Offer────  DHCP Server
Client  ──Request───►  DHCP Server
Client  ◄─Acknowledge─ DHCP Server
```

 

## 🔧 Devices Used

| Device | Model | Quantity | Purpose |
|--------|-------|:--------:|---------|
| Router | Cisco 2911 | 1 | Routes traffic between LANs and provides DHCP services |
| Switch | Cisco 2960 | 2 | Connects end devices within each LAN |
| PC | Generic PC | 4 | End-user workstations (PC1, PC2, PC4, PC5) |
| Laptop | Generic Laptop | 2 | End-user workstations (PC3 in LAN 1, PC6 in LAN 2) |




## 🖥️ Network Topology

```text
            ROUTER (Cisco 2911)
          DHCP Server for Both LANs
               /          \
          Gi0/0            Gi0/1
      192.168.10.1      192.168.20.1
            |                |
        SWITCH 1          SWITCH 2
       (Cisco 2960)      (Cisco 2960)
        /   |   \         /   |   \
      PC1  PC2  PC3     PC4  PC5  PC6

  ◄──── LAN 1 (HR) ────►  ◄── LAN 2 (Finance) ──►
```

| LAN Name | Network | Gateway | Excluded Addresses | DHCP Pool Range |
|----------|---------|---------|--------------------|-----------------|
| LAN 1 (HR) | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.1 – 192.168.10.9 | 192.168.10.10 – 192.168.10.254 |
| LAN 2 (Finance) | 192.168.20.0/24 | 192.168.20.1 | 192.168.20.1 – 192.168.20.9 | 192.168.20.10 – 192.168.20.254 |







 






 ## 📋 IP Address Plan

### Router Interfaces (manually configured)



| Interface    | IP address   | Subnetmask    | Role                      |
| ------------ | ----------      | -----------| -----------------         |
| Router Gi0/0 | 192.168.10.1 | 255.255.255.0 | Default Gateway for LAN 1 |
| Router Gi0/1 | 192.168.20.1 | 255.255.255.0 | Default Gateway for LAN 2 |



### Client Devices (addressed by DHCP)



| Device        | LAN            | IP Assignment Method | Gateway      |
|--------------|----------------|---------------------|----------------|
| PC1          | LAN 1 (HR)     | DHCP                | 192.168.10.1   |
| PC2          | LAN 1 (HR)     | DHCP                | 192.168.10.1   |
| PC3 (Laptop) | LAN 1 (HR)     | DHCP                | 192.168.10.1   |
| PC4          | LAN 2 (Finance)| DHCP                | 192.168.20.1   |
| PC5          | LAN 2 (Finance)| DHCP                | 192.168.20.1   |
| PC6 (Laptop) | LAN 2 (Finance)| DHCP                | 192.168.20.1   |





                                                           





 ## 🔴 DHCP Troubleshooting Scenarios

Three common DHCP faults were simulated, diagnosed and
resolved during this lab. Full details are in the
troubleshooting folder.

| Scenario | Cause | Fix | File |
|----------|-------|-----|------|
| PCs showing 169.254.x.x (APIPA) | DHCP service disabled | `service dhcp` + recreate pool | [APIPA Issue](https://github.com/seemasm20-source/networking-labs/blob/main/02-dhcp-configuration/troubleshooting/apipa-issues.md) |
| DHCP pool exhaustion | DHCP scope exhausted | Reviewed leases with `show ip dhcp binding` | [DHCP Pool Exhaustion](https://github.com/seemasm20-source/networking-labs/blob/main/02-dhcp-configuration/troubleshooting/dhcp-pool-exhaustion.md) |
| Duplicate IP address conflict | Static IP clashes with DHCP lease | Changed static IP to DHCP | [IP Conflict](https://github.com/seemasm20-source/networking-labs/blob/main/02-dhcp-configuration/troubleshooting/ip-conflict.md) |






 📂 Project Files





| Section              | Description                                               | File
| -------------------- | :-------------------------------------------------------: |
| Topology             | Network diagram, IP table and build steps                 |
| DHCP Config          | Full router CLI commands with explanation                 |
| APIPA Issue          | 169.254.x.x — DHCP service disabled                       |
| DHCP Pool Exhaustion | DHCP scope exhausted, no available IP addresses remaining |
| IP Conflicts         | Static IP clashing with DHCP lease                        |







 🎯  Real-World Help Desk Relevance


| Users complaint                    | Root Cause            | Fix                          |
| ---------------------------------- | --------------------- | ---------------------------- |
| Limited Connectivity / 169.254.x.x | DHCP Disabled         | Service Dhcp + Recreate Pool  |                      
| Random Disconnects                 | Duplicate IP Conflict | Change Static to DHCP        |
| New PC Has No Network Access       | Pool Exhausted        | Show IP Dhcp Binding         |
                                                                                         






 📚 Skills Demonstrated


1.Cisco 2911 router configured as DHCP server via CLI

2.Dual DHCP pool configuration — one per LAN

3.Excluded address ranges to protect network devices

4.DHCP verification using show ip dhcp binding

5.APIPA diagnosis and resolution (169.254.x.x)

6.IP address conflict root cause analysis

7.Technical documentation for GitHub portfolio





   🎓 Learning Outcome

This project provided hands-on experience configuring a Cisco router as a DHCP server across two LANs. It

demonstrated how DHCP automates IP management and strengthened understanding of common DHCP faults

directly relevant to IT Help Desk Tier 1 roles.



 ✅ Conclusion


A Cisco 2911 router was successfully configured as a DHCP server to provide automatic IP address assignment for devices across two separate LANs.

All client devices obtained valid network configurations, including IP addresses, subnet masks, default gateways and DNS server information.

The project also demonstrated practical troubleshooting by identifying, diagnosing and resolving three common DHCP-related issues:

* APIPA Addressing (169.254.x.x)

* DHCP Pool Exhaustion

* IP Address Conflict



This lab strengthened my understanding of DHCP operations, network troubleshooting, Cisco IOS configuration, and systematic problem resolution in a simulated enterprise network environment.


                   

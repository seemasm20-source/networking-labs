

# 🖥️ Topology: DHCP Configuration Lab

[Back to Project README] → [DHCP Configuration — GitHub README](https://github.com/seemasm20-source/networking-labs/blob/main/02-dhcp-configuration/README.md)





---















## 🖥️ Network Topology







**Screenshot: DHCP lab topology in Cisco Packet Tracer**










<img width="1920" height="1080" alt="Screenshot (295)" src="https://github.com/user-attachments/assets/9ade0c38-071b-4934-be9c-2e6ab0438648" />

















---


## 🔧 Devices Used

| Device | Model | Quantity | Purpose |
|--------|-------|:--------:|---------|
| Router | Cisco 2911 | 1 | Routes traffic and acts as DHCP server |
| Switch | Cisco 2960 | 2 | Connects devices within each LAN |
| PC | Generic PC | 4 | End user devices |
| Laptop | Generic Laptop | 2 | End user devices (PC3 and PC6) |

---
























## ⚙️ Step-by-Step Build Guide

### Step 1 - Add Devices to Canvas

1. Open Cisco Packet Tracer
2. Drag 1 x Router 2911 → place in the centre
3. Drag 2 x Switch 2960 → one left, one right
4. Drag 4 x PC → 2 below each switch
5. Drag 2 x Laptop → PC3 under Switch 1, PC6 under Switch 2

### Step 2 - Connect Cables

Cable type: **Copper Straight-Through** for all connections.

| From | Port | To | Port |
|------|------|----|------|
| PC1 | FastEthernet0 | Switch 1 | any FastEthernet |
| PC2 | FastEthernet0 | Switch 1 | any FastEthernet |
| PC3 (Laptop) | FastEthernet0 | Switch 1 | any FastEthernet |
| PC4 | FastEthernet0 | Switch 2 | any FastEthernet |
| PC5 | FastEthernet0 | Switch 2 | any FastEthernet |
| PC6 (Laptop) | FastEthernet0 | Switch 2 | any FastEthernet |
| Switch 1 | FastEthernet0/4 | Router | GigabitEthernet0/0 |
| Switch 2 | FastEthernet0/5 | Router | GigabitEthernet0/1 |

**Screenshot: all devices cabled, link lights green:**




























<img width="1920" height="1080" alt="Screenshot (296)" src="https://github.com/user-attachments/assets/0ecc9b7d-5e39-4d43-be1f-a4f06c3837e9" />















































---




### Step 2 -📋 IP Address Plan




### Router Interfaces (manually configured)

| Interface | IP Address | Subnet Mask | Role |
|-----------|------------|-------------|------|
| Router Gi0/0 | 192.168.10.1 | 255.255.255.0 | Default Gateway for LAN 1 |
| Router Gi0/1 | 192.168.20.1 | 255.255.255.0 | Default Gateway for LAN 2 |

### Client Devices (addressed by DHCP)

| Device | IP Address | Subnet Mask | Default Gateway |
|--------|------------|-------------|-----------------|
| PC1 | auto via DHCP | 255.255.255.0 | 192.168.10.1 |
| PC2 | auto via DHCP | 255.255.255.0 | 192.168.10.1 |
| PC3 (Laptop) | auto via DHCP | 255.255.255.0 | 192.168.10.1 |
| PC4 | auto via DHCP | 255.255.255.0 | 192.168.20.1 |
| PC5 | auto via DHCP | 255.255.255.0 | 192.168.20.1 |
| PC6 (Laptop) | auto via DHCP | 255.255.255.0 | 192.168.20.1 |

### DHCP Ranges

| LAN Name | Network | Gateway | Excluded Addresses | Planned Client Range |
|----------|---------|---------|--------------------|----------------------|
| LAN 1 (HR) | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.1 – 192.168.10.9 | 192.168.10.10 – 192.168.10.50 |
| LAN 2 (Finance) | 192.168.20.0/24 | 192.168.20.1 | 192.168.20.1 – 192.168.20.9 | 192.168.20.10 – 192.168.20.50 |

> The pool could lease up to .254, since no further exclusion was configured.

---

## 💡 Next Step

→ [DHCP Configuration](../config/dhcp-config.md)







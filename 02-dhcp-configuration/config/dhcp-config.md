# ⚙️ DHCP Configuration

  [ Back to Project README](../README.md) → [DHCP Configuration — GitHub README](https://github.com/seemasm20-source/networking-labs/blob/main/02-dhcp-configuration/README.md)

---

## 🔰 Cisco CLI Levels: Quick Reference

| Prompt | Level | How to Get There |
|--------|-------|------------------|
| `Router>` | User mode | Default when CLI opens |
| `Router#` | Privileged mode | type: `enable` |
| `Router(config)#` | Global config mode | type: `configure terminal` |
| `Router(config-if)#` | Interface mode | type: `interface GigabitEthernet0/0` |
| `Router(dhcp-config)#` | DHCP pool mode | type: `ip dhcp pool NAME` |

> **Note:** Every command only works at its correct level. If a command has no effect, check your prompt first.














## 🛠️ Complete Router Configuration

```text
Router> enable
Router# configure terminal

! --- LAN 1 interface (HR Department) ---
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.10.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

! --- LAN 2 interface (Finance Department) ---
Router(config)# interface GigabitEthernet0/1
Router(config-if)# ip address 192.168.20.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

! --- Reserve .1 - .9 for the router and network devices ---
Router(config)# ip dhcp excluded-address 192.168.10.1 192.168.10.9
Router(config)# ip dhcp excluded-address 192.168.20.1 192.168.20.9

! --- DHCP pool for LAN 1 (HR) ---
Router(config)# ip dhcp pool LAN1_POOL
Router(dhcp-config)# network 192.168.10.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.10.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit

! --- DHCP pool for LAN 2 (Finance) ---
Router(config)# ip dhcp pool LAN2_POOL
Router(dhcp-config)# network 192.168.20.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.20.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit

! --- Save configuration ---
Router(config)# end
Router# write memory
```






























<img width="1920" height="1080" alt="Screenshot (299)" src="https://github.com/user-attachments/assets/acef8c66-1f85-4795-aaa2-dad059532dcd" />












---









































## 📖 What Each CLI Command Does

| Command | Description |
|---------|-------------|
| `ip dhcp excluded-address 192.168.10.1 192.168.10.9` | Stops the router assigning these IPs to PCs |
| `ip dhcp pool LAN1_POOL` | Creates a named DHCP pool |
| `network 192.168.10.0 255.255.255.0` | Defines which network this pool serves |
| `default-router 192.168.10.1` | Pushes the gateway IP to PCs automatically |
| `dns-server 8.8.8.8` | Pushes the DNS server IP to PCs automatically |

> **Note:** The `network` command uses the **network address** (192.168.10.0 and 192.168.20.0), not the router interface IP.

---

### 🔄 Trigger DHCP on Each PC

1. Click the PC → **Desktop** → **IP Configuration**
2. Click **Static**
3. Click **DHCP** again

The PC now sends a DHCP Discover and receives its address from the router.

















## ✅ Verification

### Verification 1 - DHCP Leases

Check which addresses the router has leased to the PCs:

```text
Router# show ip dhcp binding
```

| IP Address | MAC Address | Type | Device |
|------------|-------------|------|--------|
| 192.168.10.10 | 0002.172B.6053 | Automatic | PC1 (LAN 1) |
| 192.168.10.11 | 0060.2FAC.441D | Automatic | PC2 (LAN 1) |
| 192.168.10.12 | 000A.F3AA.2B90 | Automatic | PC3 (LAN 1) |
| 192.168.20.10 | 00E0.F7DA.743B | Automatic | PC4 (LAN 2) |
| 192.168.20.11 | 00D0.FF5D.B94B | Automatic | PC5 (LAN 2) |
| 192.168.20.12 | 0090.2B20.53D5 | Automatic | PC6 (LAN 2) |

> Leases start at .10 because .1 to .9 are excluded from the pool.

**Screenshot: `show ip dhcp binding` output showing all six leases:**












<img width="1920" height="403" alt="Screenshot 1" src="https://github.com/user-attachments/assets/b7ec7ae4-7036-4f0d-aed4-ef5a4147bbb6" />





















---





















### Verification 2 - Interface Status

Check that both router interfaces are active:

```text
Router# show ip interface brief

Interface            IP-Address     OK? Method Status  Protocol
GigabitEthernet0/0   192.168.10.1   YES manual up      up
GigabitEthernet0/1   192.168.20.1   YES manual up      up
```

Both interfaces show **up / up** ✅, so the router is ready to serve DHCP on both LANs.

**Screenshot: `show ip interface brief` output showing both interfaces up:**







































<img width="1920" height="1080" alt="Screenshot (301)" src="https://github.com/user-attachments/assets/45cc07e9-d81d-4378-b2bf-6b93f122b801" />









































---


### Verification 3 - Client View

On PC1: Desktop → IP Configuration shows the IP address, Gateway and DNS received from DHCP.

**Screenshot: PC1 IP configuration (DHCP):**





<img width="963" height="969" alt="Screenshot (308)" src="https://github.com/user-attachments/assets/ce331df3-43ba-4ddf-88d7-47decd004737" />






























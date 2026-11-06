
# 🔴 IP Issue 2 - DHCP Pool Missing: Client Cannot Get IP

[ Back to Project 2 README] → [TCP/IP Network Troubleshooting - README.md](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/README.md)

---


## 📋 Problem Summary

A client was unable to obtain an IP address because the DHCP pool for its subnet had been deleted from the router configuration.

When a new client requested an IP address, the router could not provide a DHCP lease because no matching DHCP pool was configured. After failing to obtain an address, the client assigned itself an APIPA address (`169.254.x.x`).

Recreating the DHCP pool restored DHCP address allocation and allowed the client to obtain a valid IP address.

---




## 💡 What is a Missing DHCP Pool?

A missing DHCP pool failure occurs when a client requests an IP address from the router, but the router has no DHCP pool configured for that subnet, or the pool has been deleted. Without a pool, the router has no addresses to assign.

The client receives no response to its DHCP request and assigns itself an APIPA address (`169.254.x.x`) instead.

---


## 🔧 Lab Setup

### Devices Used

| Device | Model | Qty | Purpose |
|--------|-------|:---:|---------|
| Router | Cisco 2911 | 1 | Routes traffic and acts as DHCP server |
| Switch | Cisco 2960 | 1 | Connects devices within the network |
| PC | Generic PC | 2 | End-user devices (PC0 and PC1) |

### Network Details

| Device | IP |
|--------|----|
| Router G0/0 | `192.168.10.1/24` |
| PC0 | DHCP |
| PC1 | DHCP |
| DHCP pool | `192.168.10.0/24` |
| Default gateway | `192.168.10.1` |







### Step 1 - Connect the Devices

Use **copper straight-through** cables:

| From | To |
|------|----|
| PC0 FastEthernet0 | Switch Fa0/1 |
| PC1 FastEthernet0 | Switch Fa0/2 |
| Switch G0/1 | Router G0/0 |









<img width="1920" height="1080" alt="Screenshot (371)" src="https://github.com/user-attachments/assets/d7419454-700b-42c6-b98b-7b13863f2a12" />















































### Step 2 - Configure the Router Interface

```text
Router> enable
Router# configure terminal
Router(config)# interface gigabitEthernet 0/0
Router(config-if)# ip address 192.168.10.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
```














<img width="1074" height="398" alt="Screenshot (368)" src="https://github.com/user-attachments/assets/d7211ac9-99a4-4ef2-bcb2-e682acb54b8f" />































### Step 3 - Configure DHCP

```text
Router(config)# ip dhcp excluded-address 192.168.10.1 192.168.10.10
Router(config)# ip dhcp pool LAN_POOL
Router(dhcp-config)# network 192.168.10.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.10.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit
```




### Step 4 - Get IP Addresses on the PCs

On PC0 and PC1, go to **Desktop → IP Configuration → DHCP**. They should receive addresses similar to:

| Device | IP Address |
|--------|------------|
| PC0 | 192.168.10.11 |
| PC1 | 192.168.10.12 |

---





















<img width="1920" height="1080" alt="Screenshot (370)" src="https://github.com/user-attachments/assets/879a0992-0a32-4430-b9ac-40d7a8f255f0" />



















## 🧪 Create the Problem

Remove the DHCP pool from the router:

```text
Router> enable
Router# configure terminal
Router(config)# no ip dhcp pool LAN_POOL
```

Then connect a new PC (PC2) to the switch and select **DHCP** under **Desktop → IP Configuration**.

> **Note:** PC0 and PC1 may keep their previously assigned addresses until their leases need renewal. This is why a newly connected PC is used to show the failure.

---






## 🔎 Verify the Problem

PC2 sends a DHCP request, but the router cannot offer an address because the matching pool no longer exists. After the request times out, PC2 assigns itself an APIPA address (`169.254.x.x`).

**Screenshot: PC2 showing an APIPA address:**



















<img width="1920" height="1080" alt="Screenshot (372)" src="https://github.com/user-attachments/assets/97b0b372-c992-4c5b-b010-da36fe9d531c" />






















































---

# 🔧 Fix

Recreate the missing DHCP pool:

```text
Router> enable
Router# configure terminal
Router(config)# ip dhcp excluded-address 192.168.10.1 192.168.10.10
Router(config)# ip dhcp pool LAN_POOL
Router(dhcp-config)# network 192.168.10.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.10.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit
Router(config)# end
```

On PC2, go to **Desktop → IP Configuration → DHCP**. The client should now obtain a valid IP address from the restored pool.



<img width="1920" height="1080" alt="Screenshot (374)" src="https://github.com/user-attachments/assets/e5a429a0-ae43-47b8-8a9b-0a2b755f0b36" />



---



## ✅ Verification

### Verification 1 - Router

```text
Router# show ip dhcp pool
Router# show ip dhcp binding
```

### Verification 2 - PC2

```text
PC2> ipconfig /all
```

**Expected result:**

| Check | Result |
|-------|--------|
| DHCP pool | `LAN_POOL` is visible |
| IP address | PC2 receives a valid address from `192.168.10.0/24` |
| Default gateway | `192.168.10.1` |
| APIPA | PC2 no longer uses `169.254.x.x` |

**Screenshot: pool restored and PC2 receiving an address:**

<img width="1920" height="1080" alt="Router CLI after recreating the DHCP pool" src="https://github.com/user-attachments/assets/ccaac241-07de-4df1-8e87-955d5e4773b4" />



---

## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | A new client cannot get an IP address |
| **Cause** | The DHCP pool for the subnet was deleted from the router |
| **Symptom** | PC2 shows an APIPA address (`169.254.x.x`); existing clients keep their leases |
| **Tier 1** | Identifies APIPA, tries `ipconfig /release` and `/renew`, checks cable and port, escalates |
| **Tier 2** | Checks the router DHCP configuration and finds the pool missing |
| **Fix** | Recreated `LAN_POOL` with network, default gateway and DNS server |
| **Verified** | PC2 received a `192.168.10.x` address and no longer uses APIPA |


---








💡 Next Step

→ Scenario 3:- [Duplicate IP](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%202-ip%20addressing/duplicate-ip.md)

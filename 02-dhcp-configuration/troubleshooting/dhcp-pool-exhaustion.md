
# 🔴 Troubleshooting Issue 2 - DHCP Pool Exhaustion



 [ Back to Project README](../README.md) → [DHCP Configuration — GitHub README](https://github.com/seemasm20-source/networking-labs/blob/main/02-dhcp-configuration/README.md)



---

  
  
## 📋 Problem Summary

  A new PC (PC7) connected to LAN 2 (Finance) but could not receive an IP address. All addresses in the DHCP pool were already leased to existing devices, so PC7 assigned itself an APIPA     address (169.254.x.x). In this lab the pool was limited to three addresses (.10 – .12) to simulate the fault.



---






## 💡 What is DHCP Pool Exhaustion?

DHCP Pool Exhaustion occurs when all available IP addresses in a DHCP pool have been assigned to devices, leaving no free addresses for new clients.

As a result, new devices cannot obtain an IP address from the DHCP server and may experience network connectivity issues.

---




## 🔧 Create the Problem

### Step 1 - Baseline: Normal DHCP

DHCP is configured as in [DHCP Configuration](../config/dhcp-config.md). PC4, PC5 and PC6 received their addresses from the LAN 2 pool:

| Device | IP Address |
|--------|------------|
| PC4 | 192.168.20.10 |
| PC5 | 192.168.20.11 |
| PC6 | 192.168.20.12 |




<img width="1920" height="1080" alt="Screenshot (335)" src="https://github.com/user-attachments/assets/c160fe96-2fb1-4483-ab4f-355fa396be7b" />







---







### Step 2 - Shrink the Pool

Exclude the rest of the range so only three addresses remain:

```text
Router> enable
Router# configure terminal
Router(config)# ip dhcp excluded-address 192.168.20.13 192.168.20.254
Router(config)# end
```

**Screenshot: excluded range configured on the router:**











<img width="1920" height="1080" alt="Screenshot (324)" src="https://github.com/user-attachments/assets/1641303d-236c-440f-a616-2387de27fb1d" />



















---













### Step 3 - Add PC7

Connect PC7 to Switch 2, then go to **PC7 → Desktop → IP Configuration → DHCP**.

---


## 🔎 Verify the Problem

### Check the DHCP leases

```text
Router# show ip dhcp binding
```

| IP Address | Client-ID / Hardware Address | Lease Expiration | Type |
|------------|------------------------------|------------------|------|
| 192.168.20.10 | 0090.0C57.2A40 | -- | Automatic |
| 192.168.20.11 | 00E0.F969.B81C | -- | Automatic |
| 192.168.20.12 | 000D.BD58.3C5E | -- | Automatic |

> All available addresses in the pool are already leased.



### Check PC7

| Device | IP Address |
|--------|------------|
| PC4 | 192.168.20.10 |
| PC5 | 192.168.20.11 |
| PC6 | 192.168.20.12 |
| PC7 | 169.254.x.x (APIPA) |


























**Screenshot: `show ip dhcp binding` showing all three leases:**






<img width="1920" height="1080" alt="Screenshot (325)" src="https://github.com/user-attachments/assets/8f7f8701-caa2-49da-aef6-af2e8977e780" />
















**Screenshot: PC7 showing an APIPA address:**


<img width="1920" height="1080" alt="Screenshot (321)" src="https://github.com/user-attachments/assets/239a79d8-95a1-4c8b-81bf-c75271eb173a" />














---




















## 🔧 Fix

Increase the available range by reducing the excluded range:

```text
Router> enable
Router# configure terminal
Router(config)# no ip dhcp excluded-address 192.168.20.13 192.168.20.254
Router(config)# ip dhcp excluded-address 192.168.20.21 192.168.20.254
Router(config)# end
Router# write memory
```

DHCP can now assign **192.168.20.10 - 192.168.20.20**.




**Screenshot: excluded range updated on the router:**






































<img width="1920" height="1080" alt="Screenshot (328)" src="https://github.com/user-attachments/assets/0c5d4ca8-cee2-485d-9396-5b5d85f5aed4" />




---






## ✅ Verification

### Verification 1 - PC7 IP configuration

```text
PC7> ipconfig

Then renew the address on PC7:

```text
PC7> ipconfig /release
PC7> ipconfig /renew
```

| Field | Result |
|-------|--------|
| IP Address | 192.168.20.13 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.20.1 |






<img width="1920" height="1080" alt="Screenshot (336)" src="https://github.com/user-attachments/assets/b605dfcc-4fc3-4204-a94e-3bd8d375d8ff" />









### Verification 2 - DHCP leases

```text
Router# show ip dhcp binding
```

PC7 (192.168.20.13) now appears in the binding table.

**Screenshot: `show ip dhcp binding` after the fix:**








<img width="1920" height="1080" alt="Screenshot (330)" src="https://github.com/user-attachments/assets/4e5043df-c717-4096-a9e3-876e034ff56f" />







### Verification 3 - Connectivity

```text
PC7> ping 192.168.20.1
```

PC7 receives replies from the router gateway.

**Screenshot: successful ping to 192.168.20.1:**







<img width="1920" height="1080" alt="Screenshot (332)" src="https://github.com/user-attachments/assets/283e5f37-cd7a-47bf-97b2-4d913abb531c" />







## 📋 Issue Summary

| | Detail |
|---|---|
| **Issue** | New PC (PC7) cannot get an IP address |
| **Cause** | DHCP pool exhausted: all addresses already leased |
| **Symptom** | PC7 shows an APIPA address (169.254.x.x); existing devices work normally |
| **Diagnose** | `show ip dhcp binding` shows every pool address leased |
| **Fix** | Reduced the excluded range (.13 – .254 → .21 – .254) to expand the pool to .10 – .20 |
| **Verified** | PC7 received 192.168.20.13; ping to 192.168.20.1 successful |

---





## 💡 Next Step

→ [IP Address Conflict](./ip-conflict.md)






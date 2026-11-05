# 🛠️ Windows Network Commands Reference

> Run these in **Command Prompt**. Some commands (`ipconfig /release`, `/renew`, `/flushdns`, `/registerdns`) need **Run as administrator**.

---

## ipconfig

| Command | What it does |
|---------|--------------|
| `ipconfig` | Shows IP address, subnet mask and default gateway |
| `ipconfig /all` | Full details: MAC address, DHCP status, DNS servers, lease times |
| `ipconfig /release` | Releases the current DHCP address |
| `ipconfig /renew` | Requests a new DHCP address |
| `ipconfig /flushdns` | Clears the DNS cache |
| `ipconfig /displaydns` | Shows the DNS cache |
| `ipconfig /registerdns` | Refreshes DHCP leases and re-registers the PC's name in DNS |

---

## ping

| Command | What it does |
|---------|--------------|
| `ping 8.8.8.8` | Basic connectivity test |
| `ping -t 192.168.10.1` | Continuous ping (press `Ctrl + C` to stop) |
| `ping -n 20 8.8.8.8` | Sends 20 packets |
| `ping -l 1000 8.8.8.8` | Sends 1000-byte packets |
| `ping 127.0.0.1` | Tests the local TCP/IP stack |

---

## tracert

| Command | What it does |
|---------|--------------|
| `tracert google.com` | Shows every router (hop) between the PC and the destination |

A hop shown as `* * *` means that router did not answer. It does not always mean a fault.

---

## nslookup

| Command | What it does |
|---------|--------------|
| `nslookup google.com` | Name to IP address (forward lookup) |
| `nslookup 8.8.8.8` | IP address to hostname (reverse lookup) |
| `nslookup google.com 8.8.8.8` | Queries a specific DNS server |

---

## arp

| Command | What it does |
|---------|--------------|
| `arp -a` | Shows the IP-to-MAC address table. Useful for spotting duplicate IPs |

---

## netstat

| Command | What it does |
|---------|--------------|
| `netstat -an` | Shows all connections and listening ports, with numeric addresses |
| `netstat -ano` | Same as above, plus the process ID (PID) that owns each connection |

---

## route

| Command | What it does |
|---------|--------------|
| `route print` | Shows the routing table |

In the output, the **default route** has destination `0.0.0.0` and mask `0.0.0.0`. Its gateway should match your router:

```text
Network Destination    Netmask       Gateway        Interface
0.0.0.0                0.0.0.0       192.168.10.1   192.168.10.50
```

---

## Other Commands

| Command | What it does |
|---------|--------------|
| `hostname` | Shows the PC name |
| `pathping google.com` | Combines ping and tracert, and shows packet loss per hop (takes a few minutes) |

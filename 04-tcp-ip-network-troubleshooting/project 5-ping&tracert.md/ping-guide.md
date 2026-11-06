# 🏓 Ping Guide



## 💡 What is Ping?

`ping` sends a small test packet (ICMP echo request) to a destination and measures whether a reply came back and how long it took.

---

## 📖 Reading the Output

```text
C:\> ping 8.8.8.8

Reply from 8.8.8.8: bytes=32 time=12ms TTL=118
Reply from 8.8.8.8: bytes=32 time=11ms TTL=118
Reply from 8.8.8.8: bytes=32 time=13ms TTL=118
Reply from 8.8.8.8: bytes=32 time=12ms TTL=118

Ping statistics for 8.8.8.8:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 11ms, Maximum = 13ms, Average = 12ms
```

| Field | Meaning |
|-------|---------|
| `time=12ms` | Round-trip time. Lower is better |
| `TTL=118` | Time To Live: the number of router hops the packet can still pass through |
| `Lost = 0 (0% loss)` | No packet loss ✅ |

---

## ⚠️ Error Messages

| Message | Likely meaning | Next check |
|---------|----------------|------------|
| **Request timed out** | No reply. The device may be offline, or a firewall may be blocking ping | Check whether other devices reply, and check the firewall |
| **Destination host unreachable** | No route to the address, or the gateway cannot reach it | Check the IP configuration and the default gateway |
| **Ping request could not find host google.com** | The name could not be resolved, so DNS failed | Ping an IP address instead, then check DNS |
| **General failure** | A problem with the local network adapter or TCP/IP stack | Check that the adapter is enabled, then check its driver |

> A timeout does not always mean the device is down. Many devices and firewalls are set to ignore ping.

---

## 🔧 Useful Flags

| Command | What it does |
|---------|--------------|
| `ping -t 192.168.10.1` | Continuous ping, useful for catching drops (press `Ctrl + C` to stop) |
| `ping -n 20 8.8.8.8` | Sends exactly 20 packets |
| `ping -l 1000 192.168.10.1` | Sends larger packets (1000-byte buffer) |
| `ping -a 192.168.10.50` | Resolves the IP address to a hostname |

---

## 🎯 The 5-Step Diagnostic

Work from the PC outward. The first step that fails shows where the problem is.

| Step | Command | What it tests |
|:----:|---------|---------------|
| 1 | `ping 127.0.0.1` | The local TCP/IP stack |
| 2 | `ping 192.168.10.50` | The PC's own IP address (the adapter is configured) |
| 3 | `ping 192.168.10.1` | The local network and the default gateway |
| 4 | `ping 8.8.8.8` | Routing to the internet |
| 5 | `ping google.com` | DNS name resolution |




## 💡 Next Step

→ [Tracert Guide](https://github.com/seemasm20-source/networking-labs/blob/main/04-tcp-ip-network-troubleshooting/project%205-ping%26tracert.md/tracert-guide.md)

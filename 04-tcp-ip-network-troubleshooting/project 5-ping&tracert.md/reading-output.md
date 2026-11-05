# 📖 Reading Network Output

---

## ping: All Results

| Output | Status | Meaning |
|--------|:------:|---------|
| `Reply from 8.8.8.8: bytes=32 time=12ms TTL=118` | ✅ | Connected |
| `Request timed out.` | ❌ | No response (device offline, or ping blocked) |
| `Destination host unreachable.` | ❌ | No route to the address |
| `Ping request could not find host google.com.` | ❌ | DNS failed to resolve the name |
| `General failure.` | ❌ | Problem with the local adapter or TCP/IP stack |

---

## tracert: What Each Line Means

```text
C:\> tracert google.com

  1    <1 ms    <1 ms    <1 ms   192.168.10.1        ← normal
  2     8 ms     9 ms     8 ms   10.0.0.1            ← normal
  3     *        *        *      Request timed out.  ← router does not answer, route continues
  4   200 ms   210 ms   195 ms   203.45.1.1          ← high latency
  5    22 ms    21 ms    23 ms   142.250.180.46      ← destination reached
```

| Output | Status | Meaning |
|--------|:------:|---------|
| Normal times on each hop | ✅ | Traffic flows normally |
| High time on a hop | ⚠️ | A slow link or busy router. It matters only if later hops stay high too |
| `* * *` on one hop, route continues | ✅ | That router ignores the test packets, usually a firewall setting. Not a fault |
| `* * *` on every hop from one point on | ❌ | The route stops here. Check the device just before this hop |

```text
  6     *        *        *      Request timed out.
  7     *        *        *      Request timed out.   ← route stops here → problem
```

---

## ipconfig: Key Fields

| Field | Example value | Meaning |
|-------|---------------|---------|
| IPv4 Address | `192.168.10.50` | The PC's address |
| Subnet Mask | `255.255.255.0` | Defines the local network |
| Default Gateway | `192.168.10.1` | The router the PC uses to leave the network |
| DHCP Enabled | `Yes` | The address is assigned automatically |
| DNS Servers | `8.8.8.8` | The server used to resolve names |
| Lease Obtained | `[date and time]` | When DHCP assigned the address |
| Physical Address | `00-1A-2B-3C-4D-5E` | The network adapter's MAC address |

> `ipconfig /all` shows all fields. Plain `ipconfig` shows only the address, mask and gateway.

---

## nslookup: DNS Results

| Output | Status | Meaning |
|--------|:------:|---------|
| `Name: google.com` and `Address: 142.250.180.46` | ✅ | DNS is working |
| `DNS request timed out.` | ❌ | The DNS server is unreachable |
| `*** UnKnown can't find server01: Non-existent domain` | ❌ | The DNS server answered, but no record exists for that name |

```text
C:\> nslookup google.com
Server:  dns.google
Address: 8.8.8.8

Non-authoritative answer:
Name:    google.com
Address: 142.250.180.46
```

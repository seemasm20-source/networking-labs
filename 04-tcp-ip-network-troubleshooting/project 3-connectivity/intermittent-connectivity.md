
Connectivity 4 - Intermittent Connectivity


## 📋 Problem Summary

  Connection works then drops randomly. Downloads unreliable. Video calls drop. No clear pattern.




## 🔎 Verify


### Sample Output (Illustrative)

```text
C:\> ping -t 192.168.10.1

Reply from 192.168.10.1: bytes=32 time=1ms TTL=64
Reply from 192.168.10.1: bytes=32 time=1ms TTL=64
Request timed out.                              (packet dropped)
Reply from 192.168.10.1: bytes=32 time=2ms TTL=64
Request timed out.                             (dropped again!)
Reply from 192.168.10.1: bytes=32 time=45ms TTL=64

^C

Ping statistics for 192.168.10.1:
    Packets: Sent = 20, Received = 17, Lost = 3 (15% loss),
```

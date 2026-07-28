
Connectivity 4 - Intermittent Connectivity


## 📋 Problem Summary

  Connection works then drops randomly. Downloads unreliable. Video calls drop. No clear pattern.




## 🔎 Verify

Step:1

C:\> ping ipconfig /all

Verify that the active network adapter has a valid IP address, subnet mask, default gateway, DNS servers

and adapter status before investigating connectivity or packet loss.




Step:2

### 1 Sample Output (Illustrative)



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


Press CTRL + C to stop





Note: This sample output demonstrates how intermittent packet loss and increased latency may appear during troubleshooting. Actual values will vary depending on the environment.



Step:3

### 2 Sample Output (Illustrative)

Pathping combines route tracing with packet loss analysis, making it useful for identifying whether intermittent connectivity issues originate 

on the local network, within the ISP, or further along the network path.

```cmd
C:\> pathping google.com
```


```text
Tracing route to google.com [142.250.74.14]
over a maximum of 30 hops:

  0  LAPTOP-ITSUPPORT
  1  192.168.10.1
  2  10.100.0.1
  3  isp-core-router.example.net
  4  google.com [142.250.74.14]

Computing statistics for 100 seconds...

            Source to Here   This Node/Link
Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  Address
 0                                           LAPTOP-ITSUPPORT
                                0/100 = 0%   |
 1    2ms     3/100 = 3%        3/100 = 3%   192.168.10.1
                                0/100 = 0%   |
 2   10ms     3/100 = 3%        0/100 = 0%   10.100.0.1
                                2/100 = 2%   |
 3   18ms     5/100 = 5%        2/100 = 2%   isp-core-router.example.net
                                0/100 = 0%   |
 4   20ms     5/100 = 5%        0/100 = 0%   google.com

Trace complete.
```

Note: This is illustrative sample output created for documentation purposes. Actual routes, latency, hostnames, and packet loss values vary depending on the network environment.







## 🔧 Fix




   Possible Resolutions:

• Verified IP configuration using ipconfig /all.
• Tested connectivity to the default gateway using ping -t.
• Improved Wi-Fi signal by moving closer to the wireless router and using the 5 GHz band.
• Paused bandwidth-intensive applications (Windows Update, OneDrive, cloud sync).
• Updated the wireless network adapter driver.
• If packet loss continues beyond the local network, escalate to the ISP with pathping results.




## ✅ Verification

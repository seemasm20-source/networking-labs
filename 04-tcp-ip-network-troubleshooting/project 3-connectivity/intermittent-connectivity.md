
Connectivity 4 - Intermittent Connectivity


## 📋 Problem Summary

  Connection works then drops randomly. Downloads unreliable. Video calls drop. No clear pattern.




## 🔎 Verify

Step : 1

C:\> ping ipconfig /all

Verify that the active network adapter has a valid IP address, subnet mask, default gateway, DNS servers

and adapter status before investigating connectivity or packet loss.




Step : 2

### 1 Sample Output (Illustrative)

This command verifies continuous connectivity to the default gateway (router) and detect packet loss or intermittent network issues.

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



Step : 3

### 2 Sample Output (Illustrative)

Pathping combines route tracing with packet loss analysis, making it useful for identifying whether intermittent connectivity issues originate 

on the local network, within the ISP, or further along the network path.

```cmd
C:\> pathping google.com
```


```text
Tracing route to google.com [142.250.74.14]

over a maximum of 30 hops:

### Output

```text
Tracing route to google.com

over a maximum of 30 hops:

  0  LAPTOP-MN70JUKE

  1  Default Gateway

  2  ISP Router

  3  ISP Core Router

  4  * * *

Computing statistics for 75 seconds...

            Source to Here   This Node/Link

Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct

 0                               0/100 = 0%

 1    6ms     0/100 = 0%         0/100 = 0%

 2   14ms     0/100 = 0%         0/100 = 0%

 3   ---     100/100 = 100%      0/100 = 0%

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

Sample Output (Illustrative) 

C:\> ping -t 192.168.10.1

Reply from 192.168.10.1: bytes=32 time=1ms TTL=64

Reply from 192.168.10.1: bytes=32 time=1ms TTL=64

Reply from 192.168.10.1: bytes=32 time=1ms TTL=64

^C

Ping statistics for 192.168.10.1:


The continuous ping test was successful. All 30 packets sent to the destination IP address (192.168.10.1) were received successfully, resulting in 0% packet loss.

    Packets: Sent = 30, Received = 30, Lost = 0 (0% loss)

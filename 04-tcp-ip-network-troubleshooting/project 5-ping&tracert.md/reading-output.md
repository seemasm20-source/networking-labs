
## 📖 Reading Network Output


## ping - All Results



Reply from 8.8.8.8: time=12ms       ✅ connected

Request timed out                    ❌ no response

Destination host unreachable         ❌ no route

Could not find host google.com       ❌ DNS failed

General failure                      ❌ stack problem




## tracert - What Each Line Means

  2    8ms    9ms    8ms    10.0.0.1     ✅ normal
  
  4   200ms  210ms  195ms  203.45.1.1  ⚠️ high latency
  
  3    *      *      *    route continues → firewall (ok)
  
  3    *      *      *                                 
  
  4    *      *      *    ← route stops here → problem


 ##  ipconfig - Key Fields

| Field            | Value         |
| ---------------- | ------------- |
| IPv4 Address     | 192.168.10.50 |
| Subnet Mask      | 255.255.255.0 |
| Default Gateway  | 192.168.10.1  |
| DHCP Enabled     | Yes           |
| DNS Servers      | 8.8.8.8       |
| Lease Obtained   | [date]        |
| Physical Address | 00-1A-2B-3C   |



## nslookup - DNS Results

Name: google.com

Address: 142.250.180.46           ✅ working

DNS request timed out             ❌ DNS unreachable

can't find server01: Non-existent ❌ no record



## 🛠️ Windows Network Commands Reference


 ## Ipconfig


| Command               | Displayed Information               |
| --------------------- | ------------------------------------ |
| ipconfig              | IP, Mask, Gateway                    |
| ipconfig /all         | Full details + MAC, DHCP, DNS, Lease |
| ipconfig /release     | Release DHCP IP                      |
| ipconfig /renew       | Request new DHCP IP                  |
| ipconfig /flushdns    | Clear DNS cache                      |
| ipconfig /displaydns  | Show DNS cache                       |
| ipconfig /registerdns | Re-register with DNS                 |



## Ping

| Command              | What They Display           |
| -------------------- | --------------------------- |
| ping 8.8.8.8         | Basic Test                  |
| ping -t 192.168.10.1 | Continuous (Ctrl+C to Stop) |
| ping -n 20 8.8.8.8   | Send 20 Packets             |
| ping -l 1000 8.8.8.8 | 1000-Byte Packets           |
| ping 127.0.0.1       | Test Local Stack            |



## Tracert

Tracert google.com    ← trace every hop


## Nslookup

| Command                     | What They Display  |
| --------------------------- | ------------------ |
| Nslookup Google.com         | Name To IP         |
| Nslookup 8.8.8.8            | IP To Hostname     |
| Nslookup Google.com 8.8.8.8 | Query Specific DNS |


##  arp

arp -a   ← IP to MAC table — detect duplicate IPs

## netstat

netstat -an  ← all connections and listening ports

## route

route print  ← show routing table

Network Destination  Gateway 0.0.0.0            

192.168.10.1  ← default route

## Other Commands

hostname              ← display PC name

pathping google.com   ← ping + tracert combined
                        shows loss % per hop

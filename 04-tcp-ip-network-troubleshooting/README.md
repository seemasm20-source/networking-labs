
## 🌐 TCP/IP Network Troubleshooting Portfolio


**Portfolio:** IT Help Desk Tier 1 — Networking Labs

**Tool:** Windows 10/11

**Author:** Seema

**Date:**  2026





## 📌 What is This Portfolio?




Hands-on TCP/IP troubleshooting scenarios covering the full range of network connectivity issues faced in real IT Help Desk Tier 1 roles.

Every scenario documents the user complaint, root cause, step-by-step diagnosis, fix and verification.











## 📁 Portfolio Structure




| Project   | Topic                            |
| --------- | -------------------------------- |
| Project 1 | TCP/IP Fundamentals              |
| Project 2 | IP Addressing Troubleshooting    |
| Project 3 | Connectivity Troubleshooting     |
| Project 4 | Network Services Troubleshooting |
| Project 5 | Ping and Tracert Lab             |
| Project 6 | Windows Network Commands         |
| Project 7 | Real-World Scenarios             |





















## 🎯TCP /IP TROUBLESHOOTING MATRIX COVERED










| User Complaint          | Root Cause             | Project |
| ----------------------- | ---------------------- | ------- |
| No internet at all      | DNS/gateway/cable      | P3 + P7 |
| PC shows 0.0.0.0        | DHCP not responding    | P2      |
| PC shows 169.254.x.x    | APIPA -DHCP failed     | P2      |
| IP works name fails     | DNS problem            | P3      |
| Same-LAN PC unreachable | Firewall blocking ping | P3      |
| Internet randomly drops | Packet loss- cable     | P3      |
| Cannot ping gateway     | Wrong gateway / cable  | P3      |
| Cannot RDP to server    | Port 3389 blocked      | P4      |
| Cannot print            | Printer IP changed     | P7      |
| Shared folder error     | Port 445 blocked       | P7      |
| One website fails       | Stale DNS cache        | P7      |
| Slow internet           | Packet loss-pathping   | P7      |





















## 📋 Key Commands Quick Reference




| Command            | Purpose                                |
| ------------------ | -------------------------------------- |
| ipconfig /all      | Full IP config -check IP, gateway, DNS |
| ping 127.0.0.1     | Test local TCP/IP stack                |
| ping [gateway]     | Test local network                     |
| ping 8.8.8.8       | Test internet without DNS              |
| ping -t [IP]       | Continuous ping -catch drops           |
| tracert [dest]     | Trace route -find where it breaks      |
| pathping [dest]    | Detailed packet loss per hop           |
| nslookup [name]    | Test DNS resolution                    |
| arp -a             | Show IP to MAC table                   |
| netstat -an        | Show active connections and ports      |
| route print        | Show routing table                     |
| ipconfig /flushdns | Clear DNS cache                        |
| ipconfig /release  | Drop DHCP IP                           |
| ipconfig /renew    | Get new DHCP IP                        |






















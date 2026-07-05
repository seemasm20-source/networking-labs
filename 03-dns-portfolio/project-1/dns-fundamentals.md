

## 📖 Project 1- DNS Fundamentals





## 💡 What is DNS?

    DNS stands for Domain Name System. Every website has an IP address like 142.250.180.46. 

    Humans cannot remember number strings. DNS translates names into numbers.





    You type    : www.google.com
DNS converts: www.google.com → 142.250.180.46
Browser goes: to 142.250.180.46 → page loads





## 🔄 How DNS Works - Step by Step



Step 1 — You type www.google.com in browser

Step 2 — PC checks local DNS cache first

Step 3 — If not cached, asks configured DNS server

Step 4 — DNS server returns IP: 142.250.180.46

Step 5 — PC connects to that IP

Step 6 — Website loads












## 📚 Key DNS Terms




| Term           | Short Description                   |
| -------------- | ----------------------------------- |
| DNS Server     | Answers 'what IP is this name?'     |
| A Record       | Maps hostname to IPv4 address       |
| CNAME          | Alias - one name points to another  |
| PTR Record     | Reverse lookup -IP to name         |
| DNS Cache      | Saved answers from previous lookups |
| TTL            | How long a DNS answer stays cached  |
| Forward Lookup | Name → IP address                   |
| Reverse Lookup | IP address → Name                   |










## 🔑 Core DNS Commands



1. C:\> ipconfig /all
 
Shows DNS server currently on your PC

2. C:\> nslookup google.com
 
Queries DNS — returns IP for that name

3. C:\> ping google.com     ← uses DNS to resolve first
 
C:\> ping 8.8.8.8        ← bypasses DNS completely

Key rule:

ping by IP works + ping by name fails = DNS problem

4. C:\> ipconfig /displaydns   ← view cache
 
C:\> ipconfig /flushdns     ← clear cache










## 🎯 Why DNS Matters for Tier 1



| User Complaint               | DNS Cause                   |
| ---------------------------- | --------------------------- |
| Cannot open any website      | DNS server down             |
| Intranet not loading         | Internal DNS not configured |
| Ping by IP works, name fails | DNS record missing          |
| Website looks outdated       | Stale DNS cache             |
| Internet broken after change | DNS server IP changed       |

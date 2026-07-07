
## 🔍 Cache - ipconfig /displaydns


## 📋 What is ipconfig /displaydns?

ipconfig /displaydns displays all DNS records currently stored in the local DNS cache. 

These cached entries contain recently resolved domain names and their corresponding IP addresses, 

allowing Windows to resolve names faster without contacting the DNS server for every request.





How to Run

C:\> ipconfig /displaydns



## 📖 Reading the Output

    google.com
    ----------------------------------------
    Record Name . . . . :   google.com
    
    Record Type . . . . :  1          
    
    Time To Live  . . . . :  127

    Data Length . . . . :   16

    Section  . . . . :      Answer
    
    A (Host) Record . . . . :  142.251.14.113







| **Field**              | **Description**                                                                                                                          |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **Record Name**        | The domain name stored in the local DNS cache (for example, `www.google.com`).                                                           |
| **Record Type**        | Identifies the DNS record type. For example, **1 = A (Host) Record**, which maps a hostname to an IPv4 address.                          |
| **Time To Live (TTL)** | The remaining time, in seconds, that Windows keeps the DNS record in its local cache before it expires and a new DNS lookup is required. |
| **Data Length**        | The size of the DNS record data in bytes. For an **A record**, the value is **4 bytes** because an IPv4 address is 32 bits long.         |
| **Section**            | Indicates which section of the DNS response the record belongs to. **Answer** means the record directly answers the DNS query.           |
| **A (Host) Record**    | Displays the IPv4 address associated with the hostname.                                                                                  |
























<img width="1920" height="1080" alt="Screenshot (360)" src="https://github.com/user-attachments/assets/2db688d5-d748-4379-9ba5-99b1eaf48f66" />




























































 **Note:** Many websites, including Google, support both **IPv4** and **IPv6**. When Windows performs a DNS lookup for these websites, 
 
 it may cache both **A (IPv4)** and **AAAA (IPv6)** records if they are returned by the DNS server. 
 
 As a result, `ipconfig /displaydns` can display both record types in the local DNS cache.






























## 🎯Practical use cases of ipconfig/ displaydns:




 | Situation                       | Displaydns Reveals             |
| ------------------------------- | ------------------------------ |
| User sees wrong website version | Old IP cached-needs flushdns |
| New server unreachable by name  | Negative cache entry stored    |
| Works for some staff not others | Cache difference between PCs   |


    

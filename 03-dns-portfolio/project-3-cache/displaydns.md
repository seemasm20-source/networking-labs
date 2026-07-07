
## 🔍 Cache — ipconfig /displaydns


## 📋 What is ipconfig /displaydns?

ipconfig /displaydns displays all DNS records currently stored in the local DNS cache. 

These cached entries contain recently resolved domain names and their corresponding IP addresses, 

allowing Windows to resolve names faster without contacting the DNS server for every request.





How to Run

C:\> ipconfig /displaydns



📖 Reading the Output

    google.com
    ----------------------------------------
    Record Name . . . . : google.com
    
    Record Type . . . . : 1          
    
    Time To Live  . . . : 127

    Data Length . . . :  16

    Section . . . :     Answer
    
    A (Host) Record . . : 142.251.14.113


    | Field                  | Meaning                                                               |
| ---------------------- | --------------------------------------------------------------------- |
| **Record Name**        | The domain name stored in the DNS cache (`www.google.com`).           |
| **Record Type**        | `1` = **A Record**, which maps a hostname to an IPv4 address.         |
| **Time To Live (TTL)** | The number of **seconds remaining** before this cached entry expires. |
| **Data Length**        | The size of the DNS record data in **bytes**.                         |
| **Section**            | Indicates which part of the DNS response the record came from.        |
| **A (Host) Record**    | The IPv4 address returned by the DNS server.                          |























<img width="1920" height="1080" alt="Screenshot (360)" src="https://github.com/user-attachments/assets/2db688d5-d748-4379-9ba5-99b1eaf48f66" />











































 **Note:** Many websites, including Google, support both **IPv4** and **IPv6**. When Windows performs a DNS lookup for these websites, 
 
 it may cache both **A (IPv4)** and **AAAA (IPv6)** records if they are returned by the DNS server. 
 
 As a result, `ipconfig /displaydns` can display both record types in the local DNS cache.























 🎯When it mostly used:




 | Situation                       | Displaydns Reveals             |
| ------------------------------- | ------------------------------ |
| User sees wrong website version | Old IP cached — needs flushdns |
| New server unreachable by name  | Negative cache entry stored    |
| Works for some staff not others | Cache difference between PCs   |


    

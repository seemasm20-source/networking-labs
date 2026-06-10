
Troubleshooting Issue-1



Scenario : 1 



Issue : Devices in different LANs were unable to communicate.


Cause : Router interface GigabitEthernet0/0 was Administratively shut down.



  Router(config)# interface GigabitEthernet0/0

  

  Router(config-if)# shutdown




What is shutdown/ Administratively down means in Router CLI?





In a router CLI (such as Cisco IOS), "Administratively Down" means an interface has been manually disabled by a network administrator using the shutdown command, or it has never been enabled. It will not pass traffic until re-enabled.
























<img width="1920" height="1080" alt="Screenshot (229)" src="https://github.com/user-attachments/assets/271234a7-dc65-4d3b-9157-e0a00b76f1fd" />





















  



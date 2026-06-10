
Troubleshooting Issue-1



Scenario : 1 



Issue : Router Interface Was Administratively Down



Cause : The router interfaces were disabled manually



  Router(config)# interface GigabitEthernet0/0

  

  Router(config-if)# shutdown




What is shutdown/ Administratively down means in Router CLI?





In a router CLI (such as Cisco IOS), "Administratively Down" means an interface has been manually disabled by a network administrator using the shutdown command, or it has never been enabled. It will not pass traffic until re-enabled.


  



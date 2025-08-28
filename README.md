# Router-and-Switch-Configuration
 CLI Configuration Modes
The basic CLI modes that we will be referring to below are as follows:
Router> <– User EXEC Mode (Default mode when you log in to the router CLI)
Router#	<– Privileged EXEC mode (Enter <enable> to get into this mode)
Router(config)#	<– Global Configuration Mode (enter <configure terminal> to switch to this mode)
Router(config-if)# <– Interface Configuration Mode 
Router(config-line)# <– Line Configuration Mode

#Commands 
#Switch to the global config mode
STEP1
Set up a router password ----> enable secret <your password>

STEP2
Configure Hostname ----> hostname <your hostname>

STEP3

#Configure IP address for the interface you need to switch to the interface mode
To configure the internal interface ---> interface GigabitEthernet 0/0
Configure ip address ---> ip address <ip address x subnet mask>
                    ----> no shutdown
                    ----> exit

To configure the external interface ---> interface GigabitEthernet 0/1
Configure ip address ---> ip address <ip address x subnet mask>
                    ----> no shutdown
                    ----> exit  
                    ----> wr
STEP4 
Configure Routing (Static or Dynamic) switch back to global config mode
To set static route ---> ip route <destination network> <subnet mastk> <gateway>
                   ----> ip route 200.200.200.0 255.255.255.0 100.100.2
                   ----> exit
                   
STEP5 
Save your configuration
To enable your configuration ----> copy running-config startup-config
To display or verify your config or setting ---> show running-config

STEP6 
Configure NAT
This is important if your router acts as your internet border gateway to provide access to the internal private LAN to the internet
My-Router(config)# conf term
          --------> interface GigabitEthernet 0/0
          --------> ip nat outside
          --------> exit
My-Router(config)# interface GigabitEthernet 0/1
          --------> ip nat inside
          --------> exit

STEP7 
Configure NAT for access control list
Now we need to create an Access List which will identify which specific traffic will be
translated using NAT. Assuming that the internal LAN network is 192.168.10.0/24 :

My-Router(config)# access-list 1 permit 192.168.10.0 0.0.0.255
My-Router(config)# ip nat inside source list 1 interface GigabitEthernet 0/0 overload

STEP8
Configure DHCP
A Cisco router can be configured as a DHCP server to assign IP addresses dynamically
to internal hosts. In privileged EXEC mode. Configure the DHCP pool to assign addresses to internal hosts
my-router# ------>ip dhcp pool lan-pool
                  network 192.168.10.0 255.255.255.0
                  default-router 192.168.10.1
                  dns-server 8.8.8.8

Then, exclude which IP addresses you don’t want to be assigned by the router:
Do not assign addresses 1 to 50

ip dhcp excluded-address 192.168.10.1 192.168.10.50






  







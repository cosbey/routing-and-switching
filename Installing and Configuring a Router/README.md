# Installing and Configuring a Cisco Router

## Lab Objective: 
Learn how to install a branch office and HQ router. 

## Lab Purpose: 
Routers can take several hours to install and configure. This lab will cover just a few of the basic steps you need to follow to connect your router in a branch office (R1) and your HQ (R0). I’ve scaled everything down for simplicity.

## Lab Tool: 
Packet Tracer 

## Lab Topology: 
Please use the following topology to complete this lab exercise:

![Pasted image 20230703150828](https://github.com/cosbey/routing-and-switching/assets/32424700/e3691c5d-8537-4d23-b10f-9e2b58d70ff6)


## Task 2:
Change the hostname on the router and then check the interfaces for the correct name/number/slot so you configure the correct one. You will use a serial cable to connect the two routers.


![Pasted image 20230703153307](https://github.com/cosbey/routing-and-switching/assets/32424700/22ef5300-a511-4349-a58d-7e256df18f54)

## Task 2:
One of the routers will have a DCE cable end. This provides the clocking for the connection, so you need to add a speed command. The `show controllers interface X` command will tell you which cable type you have. Packet Tracer appears to automatically add a clock rate, so we need not worry about that step, but bear it in mind for live routers or remote racks.

![Pasted image 20230703153909](https://github.com/cosbey/routing-and-switching/assets/32424700/0bb95497-e51b-453f-a256-47aefb5085cb)

Let's evaluate each line step by step:

1. `Router#conf t`: This command is used to enter global configuration mode. The prompt changes from "`Router#`" to "`Router(config)#`". Global configuration mode allows you to configure various settings on the router.

2. `Router(config)#hostname R0`: This command sets the hostname of the router to "`R0`". The hostname is a user-defined label that helps identify the device in a network. After executing this command, the prompt changes to "`R0(config)#`".

3. `Router(config)#exit`: This command is used to exit the current configuration mode and return to the previous mode, which in this case is privileged EXEC mode. The prompt changes from "`R0(config)#`" to "`R0#`".

4. `R0#show ip int brief`: This command is used to *display a brief summary of the router's IP interfaces*. It provides information such as the interface name, IP address, status, and protocol. Executing this command displays the summary information on the console.


## Task 3:
Configure the IP address on either router and then ping across the link.

![Pasted image 20230703155119](https://github.com/cosbey/routing-and-switching/assets/32424700/cd06ce6e-1f7e-4f56-88ba-9bc88ac807c7)

![Pasted image 20230703155304](https://github.com/cosbey/routing-and-switching/assets/32424700/7d7af15f-ba61-4fe7-9596-4cd93f91ed23)


## Task 4:
Configure the Ethernet interfaces on the routers and add the IP addresses and default gateways on the hosts. Here is the config for R0. On R1 remember that it’s using the 192.168.1.0 network on the LAN side.

#### Router 0
![Pasted image 20230703180224](https://github.com/cosbey/routing-and-switching/assets/32424700/d87f6590-ca45-41e0-8dbe-53d61aeb31d3)

#### Router 1
![Pasted image 20230703180409](https://github.com/cosbey/routing-and-switching/assets/32424700/bd35572d-5bab-43a0-b71f-e83e8be05cc2)

*Note: Configure endpoint devices with the proper IP configuration for each PC.*
![Pasted image 20230703180757](https://github.com/cosbey/routing-and-switching/assets/32424700/eb65d4e5-e5c2-4b3b-a811-9cf8b2ebf265)

## Task 5: 
Configure RIP version 2 on the network so that each router has a map of the entire topology.

#### Router 0

![Pasted image 20230703192037](https://github.com/cosbey/routing-and-switching/assets/32424700/e047bccd-1e7b-4fa9-8a4d-a62d0f1882b4)

![Pasted image 20230703182048](https://github.com/cosbey/routing-and-switching/assets/32424700/8ce63379-d963-48cc-924d-006314d56656)

#### Router 1

![Pasted image 20230703192153](https://github.com/cosbey/routing-and-switching/assets/32424700/451ca2d4-be28-4268-9706-f68289fd1d78)

![Pasted image 20230703182153](https://github.com/cosbey/routing-and-switching/assets/32424700/56714e74-c1a3-4090-9ab9-dd1bc6c1195e)

Let's evaluate each line step by step:

1. `R1(config)#router rip`: This command enters router configuration mode and specifies that the device will be running the Routing Information Protocol (RIP) as its routing protocol.

2. `R1(config-router)#ver 2`: This command sets the RIP version to 2. By specifying version 2, the device will use the enhanced features and improvements of RIP version 2 over the older version 1.

3. `R1(config-router)#network 10.0.0.0`: This command specifies that the network with the IP address range of 10.0.0.0 should be included in the RIP routing process. The exact subnet mask is not specified in this command.

4. `R1(config-router)#net 192.168.1.0`: This command specifies that the network with the IP address range of 192.168.1.0 should also be included in the RIP routing process. Again, the exact subnet mask is not specified here.

5. `R1(config-router)#end`: This command exits the router configuration mode and returns to privileged EXEC mode.


## Task 7:
Ping the remote PC from one end to the other:

![Pasted image 20230703183321](https://github.com/cosbey/routing-and-switching/assets/32424700/5447cd74-c0f3-4a9e-9e54-bd8d55c1f06e)

## Task 8:
Configure R0 to allow remote access via Telnet. Add a username and password so the administrator can telnet to the router. Add an enable password so that the admin can get into enable mode to do any configurations. The command `login local` tells the router to check the user against the local database of usernames and passwords. Then test your connection from the PC.

![Pasted image 20230703183953](https://github.com/cosbey/routing-and-switching/assets/32424700/2282c3cf-fe32-48c4-8664-9ade3ae86d39)

#### Telnet from 192.168.1.2:
![Pasted image 20230703184441](https://github.com/cosbey/routing-and-switching/assets/32424700/628a71bc-3ca1-4bf2-bc81-c615f6f43867)

Let's evaluate each line step by step:

1. `R0#conf t`: This command is used to enter *global configuration mode*. The prompt changes from "`R0#`" to "`R0(config)#`". *Global configuration mode* allows you to configure various settings on the router.

2. `R0(config)#enable secret hello`: This command sets the enable secret password to "`hello`". The enable secret password is used to protect access to *privileged EXEC mode*. It is more secure than the enable password as it is encrypted using a strong hashing algorithm.

3. `R0(config)#username cosbey password cisco`: This command creates a local user account with the username "`cosbey`" and the password "`cisco`". *This user account can be used for authentication purposes, such as for remote access or administrative login.*

4. `R0(config)#line vty 0 15`: This command enters line configuration mode for `virtual terminal lines` (vty) 0 to 15. *VTY lines are used for remote access to the router*.

5. `R0(config-line)#transport input telnet`: This command specifies that remote access to the router via the vty lines will be allowed using the Telnet protocol. `Telnet is a legacy protocol and is less secure than SSH.`

6. `R0(config-line)#login local`: This command `enables local authentication` for the vty lines. It means that when someone tries to access the router via Telnet, they will be prompted for a username and password configured locally on the router.




## Observations and Results:

When creating a network it is much easier to visualize where your going than to build it from scratch right away. I found that creating a design early on in this process is critical in determining where you are going. Once documented, we can essentially build out the design one device at a time. We started by identifying the hostnames and IP address first, for our routers. Later, we built a network `(10.0.0.0)` between the two routers by utilizing the serial interfaces from each. Overall, I believe this lab is a great place to start for understanding the basic fundamentals of routing in a Cisco environment.


## Lessons Learned:

In this lab, we have used basic Cisco commands to:

- identify interfaces on a router,
- configure IP addresses,
- configure Ethernet interfaces,
- configure RIPv2 on a network, and
- enable remote access via telnet.

**Additional Resources:** 
- https://www.netacad.com/courses/packet-tracer
- https://www.gns3.com/


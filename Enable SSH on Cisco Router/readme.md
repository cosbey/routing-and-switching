**Lab Objective:** The objective of this lab exercise is for you to learn and understand how to enable SSH access to a device—in this case, a Cisco router. 

**Lab Purpose:** It’s never a good idea to permit Telnet access to network devices, especially in corporate settings. SSH is a secure way to connect to network devices. 
In order to configure SSH you need to: 

1. Create a hostname. 
2. Create a domain name. 
3. Generate a crypto key. 

**Lab Tool:** Packet Tracer or GNS3

**Lab Topology:** Please use the following topology to complete this lab exercise:


![Pasted image 20230622224538](https://github.com/cosbey/routing-and-switching/assets/32424700/b2c8eb1b-2280-47bd-b00b-b14aaba7bf29)


**Task 1:** Drag two routers onto the canvas. I don’t point this out in the labs because I presume you know this from reading your theory books, but connecting routers together requires a crossover cable (because we aren’t using a switch). I used 1941 models for this lab, but for most of the others I used 1841 models (which have Fast Ethernet interfaces).

![Pasted image 20230622235724](https://github.com/cosbey/routing-and-switching/assets/32424700/b1a6257f-90c6-48a4-bc5c-8837950434f7)


**R1>enable:** *This command is used to enter privileged EXEC mode, which provides access to all configuration commands on the Cisco device. After entering this command, the prompt changes from "R1>" to "R1#".*
    
**R1#conf t:** *This command is used to enter global configuration mode, where you can configure various settings on the device. After entering this command, the prompt changes to "R1(config)#".*

**Task 2:** 
Add an IP address to each Ethernet interface and ‘no shut’ them in order to bring them up. 
- `R0(config)#interface g0/0` 
- `R0(config-if)#ip address 192.168.1.1 255.255.255.0`
- `R0(config-if)#no shut `
*%LINK-5-CHANGED: Interface GigabitEthernet0/0, changed state to up*

**Over to Router1:** 
- `R1(config)#interface g0/0` 
- `R1(config-if)#ip address 192.168.1.2 255.255.255.0` 
- `R1(config-if)#no shut` 
%LINK-5-CHANGED: Interface GigabitEthernet0/0, changed state to up 
- `R1(config-if)#end`

**Make sure you can ping across the link.** 
`R1#ping 192.168.1.1` 
*Type escape sequence to abort. Sending 5, 100-byte ICMP Echos to 192.168.1.1, timeout is 2 seconds: .!!!! Success rate is 80 percent (4/5), round-trip min/avg/max = 0/0/0 ms*


 
![Pasted image 20230622232042](https://github.com/cosbey/routing-and-switching/assets/32424700/2696fae5-decc-414a-84c5-f52651e637d2)


**Task 3:** 
Secure Router1 so that it accepts SSH incoming connections. We need to set a domain name and generate keys. As options, we have set retries for the password to 2 attempts and a timeout of 60 seconds if there is no activity.

![Pasted image 20230622233735](https://github.com/cosbey/routing-and-switching/assets/32424700/daa33ec8-a9d4-497d-8e57-8acbfed88d35)


- **R1(config)#ip domain-name 101.labs.net:** *This command sets the domain name for the device to "101.labs.net".* This domain name can be used for various services such as generating SSL certificates.
    
- **R1(config)#crypto key generate rsa:** *This command generates an RSA key pair for the device, which is used for secure communication protocols such as SSH.* The name of the keys will be "R1.101.labs.net".
    
- **How many bits in the modulus [512]: 1024:** *This prompt is asking for the desired key modulus size.* In this case, the user chooses to generate a 1024-bit RSA key.
    
- **R1(config)#ip ssh time-out 60:** *This command sets the SSH timeout value to 60 minutes. After 60 minutes of inactivity, the SSH session will be terminated.*
    
- **R1(config)#ip ssh authentication-retries 2:** *This command sets the maximum number of authentication retries for SSH to 2. If authentication fails twice, the SSH connection will be terminated.*

**Task 4:** Connect to Router1 from Router0 using SSH. You should be prompted for the password, which, as you can see above, is ‘cisco’. You can add a username for the connection, which I’ve done here. Use the letter ‘l’ below after ‘ssh’ not the number 1.

![Pasted image 20230622235437](https://github.com/cosbey/routing-and-switching/assets/32424700/fe294a5e-42ac-4e1d-b414-66c9d0f55d14)




**Task 5:** Attempt to telnet from Router0 to Router1 to check that the connection is refused.

![Pasted image 20230622234519](https://github.com/cosbey/routing-and-switching/assets/32424700/714d46f1-e9f7-4852-a5af-326b825638d1)

**Observations and Results:** I found that this lab -- albeit simple-- was extremely useful in explaining some basic concepts of SSH fundamentals. Also, utilizing the command line to create connections between the router interfaces demonstrated value as well. These concepts build on each other while also teaching and understanding how these concepts work in totality.

**Lessons Learned:** In this lab I learned:
- How to establsh connectivity between router interfaces
- Create a hostname and domain for the routers
- Install and establish SSH connectivity

**Additional Resources:** 
- https://www.netacad.com/courses/packet-tracer
- https://www.gns3.com/





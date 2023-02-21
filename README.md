<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we distinguish different network traffic from Azure Virtual Machines with Wireshark as well as evaluate with Network Security Groups. <br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Actions and Observations</h2>

<p>
</p>
<p>
Hey! Welcome to my tutorial on performing activities with Network Security Groups and Inspecting Network Protocols. On the Azure Portal we will create two virtual machines (VM's) Before we create the VM's we will have to create a resource group. Name the resource group whatever you'd like. One machine will be a Linux machine and the other will be a Windows 10 machine. Both must be on the same Vnet. Let's now connect to the Windows virtual machine using remote desktop. Within the virtual machine, we will download Wireshark. We can just go on Google and search up Wireshark and install it. Then we open up Wireshark and filter for ICMP traffic only. ICMP is a network layer protocol that relays messages concerning network connection issues. Ping uses this and ping tests the connectivity between hosts. Retreive the private IP address from the Ubuntu VM and we will ping it from within the Windows virtual machine.
</p>
<br />
<p>
<img src="https://i.imgur.com/l5q0FCR.jpg" height="80%" width="80%"/>
</p>
<p>
</p>
<br />
<p>
</p>
<p>
Now we will attempt to initiate a perpetual non-stop ping from our Windows 10 VM to our Ubuntu VM. This will result in the ping continuously pinging until we decide to stop it. While our Windows is continuing to ping our Ubuntu machine we have to go back to the Azure Portal and go to our Ubuntu machine and block inbound ICMP traffic on the machine's firewall. After that is complete echo replys from the Ubuntu machine will force it to stop. We will block ICMP by basically creating a new Network Security Group on the Ubuntu machine that will be forced to block the ICMP. We can call the rule "DENY_ICMP_TRAFFIC ''. When we go back to our VM and see the ping timing out we can go back and enable ICMP and watch the ping start to ping again.
</p>
<br />
<img src="https://i.imgur.com/u7RRHLe.jpg" height="80%" width="80%"/>
</p>
<img src="https://i.imgur.com/0IOxktm.jpg" height="80%" width="80%"/>
<p>
Back into Wireshark, let's filter for SSH Traffic only. We will capture SSH packets only. Using the Ubuntu virtual machine's private IP address, we will SSH into the Ubuntu machine with the command prompt "ssh labuser@10.0.0.5" After we do this we can view Wireshark starts to capture SSH packets very rapidly. 
</p>
<br />
<img src="https://i.imgur.com/b5Zk7SQ.jpg" height="80%" width="80%"/>
</p>
<p>
Back into Wireshark again, let's filter for DHCP Traffic. DHCP is the Dynamic Host Configuration Protocol which works on ports 67/68. It is used to automatically assign IP addresses to machines. From our Windows 10 VM we wil basically request a new IP address with the command saying "ipconfig/renew '' After this command we now observe the DHCP Traffic showing in Wireshark.
</p>
<br />
<img src="https://i.imgur.com/oEpJn2T.jpg" height="80%" width="80%"/>
</p>
<p>
Awesome, let's filter for DNS Traffic now. Set wireshark to filter DNS traffic. Commence DNS traffic by typing in the command "nslookup www.google.com" or "nslookup www.disney.com" the command naturally is responsible for translating domain names into specific IP addresses. 
</p>
<br />
<img src="https://i.imgur.com/NpO3QHG.jpg" height="80%" width="80%"/>
</p>
<p>
Last but not least let's filter for RDP Traffic. Enter tcp.port==3389 the traffic is non-stop spamming due to the fact that we are using Remote Desktop Protocol to connect to our VM and is constantly showing a livestream from one computer to another so traffic is always showing and essentially being transmitted. 
</p>
<br />
<img src="https://i.imgur.com/VSNJwR6.jpg" height="80%" width="80%"/>
</p>
<p>


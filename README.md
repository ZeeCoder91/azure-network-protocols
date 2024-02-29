<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create your resource group (1x Windows VM, 1x Ubuntu VM, and subnet)
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic
  

<h2>Actions and Observations</h2>

<p>
Create a Resource Group. Create a Windows 10 Virtual Machine and while creating the VM, select the previously created Resource Group and allow it to create a new Virtual Network (Vnet) and Subnet. Then, create a Linux (Ubuntu) and select the previously created Resource Group and Vnet. Observe Your Virtual Network within Network Watcher (as seen in abpve photo).
</p>
<p>
<img src="https://i.imgur.com/Ks4Q5bz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Grab your Public IP Address from Microsoft Azure.
</p>
<p>
<img src="https://i.imgur.com/70uIcho.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
  Use Remote Desktop into your Windows 10 virtual machine. 
</p>
<p>
<img src="https://i.imgur.com/MCYXVTO.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Download and Intall Wireshark with all the default settings. 
</p>
<p>
<img src="https://i.imgur.com/IRnG3zV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Open Wireshark and filter for ICMP traffic only.
</p>
<p>
<img src="https://i.imgur.com/s5YdUbp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM</p>
<p>
<img src="https://i.imgur.com/i9j2yWr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Observe ping requests and replies within WireShark
</p>
<p>
<img src="https://i.imgur.com/tkh1mxR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
</p>
<p>
<img src="https://i.imgur.com/tVT63iN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic:
</p>
<img src="https://i.imgur.com/cPtvwBx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<p>
<img src="https://i.imgur.com/sGPk8xi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
<img src="https://i.imgur.com/ahYxBPv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
<img src="https://i.imgur.com/psYL8UN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
</p>
<p>  
<img src="https://i.imgur.com/6IkGjgN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using
</p>
<p>
<img src="https://i.imgur.com/hLvCuMG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
</p>
<p>
<img src="https://i.imgur.com/xa3wpqq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Stop the ping activity
</p>
<p>
<img src="https://i.imgur.com/5vh29Fb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Back in Wireshark, filter for SSH traffic only:
</p>
<p>
<img src="https://i.imgur.com/YVan6HT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
From your Windows 10 VM, “SSH into” the Ubuntu Virtual Machine (via its private IP address) and notice the activity that occurs in Wireshark when entering the password to connect to the Ubuntu VM</p>
<p>
<img src="https://i.imgur.com/BMzNR4K.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p> 
  Observe the activity that occurs once successfully connected into Ubuntu.</p>
<p>
<p>
<img src="https://i.imgur.com/nkK8e9P.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
  Exit the SSH connection by typing ‘exit’ and pressing [Enter]
</p>

<img src="https://i.imgur.com/a0mufR0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Back in Wireshark, filter for DHCP traffic only
</p>
<p>
<img src="https://i.imgur.com/ikQdqx1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
Observe the DHCP traffic appearing in WireShark
</p>
<p>
<img src="https://i.imgur.com/KcW8DrY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Back in Wireshark, filter for DNS traffic only
</p>
<p>
<img src="https://i.imgur.com/tGO1eSE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
</p>
<p>
<img src="https://i.imgur.com/YMpASho.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Observe the DNS traffic being show in WireShark
</p>
<p>
<img src="https://i.imgur.com/AZkQiix.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Back in Wireshark, filter for RDP traffic only (tcp.port == 3389). Observe the immediate non-stop spam of traffic
</p>
<p>
<img src="https://i.imgur.com/n2m7GY8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Notice the RDP (protocol) is constantly showing a live stream from one computer to another, which is why the traffic is always being transmitted.
</p>
<p>
<img src="https://i.imgur.com/yxHKPOd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
<img src="https://i.imgur.com/UDawVdl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

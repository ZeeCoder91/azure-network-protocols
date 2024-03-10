<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<!--- <h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com) --->

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
First, create a Resource Group in Azure to organize your resources. Next, set up a Windows 10 Virtual Machine (VM). During setup, choose the Resource Group you made earlier and let Azure create a new Virtual Network (Vnet) and Subnet for this VM. After that, create a Linux (Ubuntu) VM, again selecting the same Resource Group and this time, the existing Vnet. Finally, use Network Watcher in Azure to view and check the setup of your Virtual Network, ensuring both VMs are correctly configured and connected within the same network. This step helps manage and monitor your virtual network environment efficiently.</p>
<p>
<img src="https://i.imgur.com/Ks4Q5bz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Find and jot down your Public IP Address from the Microsoft Azure portal.
</p>
<p>
<img src="https://i.imgur.com/70uIcho.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>Connect to your Windows 10 virtual machine using Remote Desktop.
</p>
<p>
<img src="https://i.imgur.com/MCYXVTO.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Download and install Wireshark, accepting the default settings throughout the installation process.</p>
<p>
<img src="https://i.imgur.com/IRnG3zV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Launch Wireshark, then enter "icmp" into the filter bar to exclusively display ICMP traffic.</p>
<p>
<img src="https://i.imgur.com/s5YdUbp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Locate the private IP address of your Ubuntu Virtual Machine. Next, on your Windows 10 Virtual Machine, open the Command Prompt and send a ping request to the Ubuntu VM using its private IP address.<p>
<img src="https://i.imgur.com/i9j2yWr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Monitor the ping requests and their responses in Wireshark by observing the captured ICMP traffic.</p>
<p>
<img src="https://i.imgur.com/tkh1mxR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
<p>Start a continuous ping to the Ubuntu VM by executing <code>ping -t [Ubuntu VM's IP address]</code> from your Windows 10 VM. This command keeps the ping active without stopping.</p>
<p>
<img src="https://i.imgur.com/tVT63iN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>Go to the Network Security Group settings for your Ubuntu VM in Azure. Find the rules for incoming traffic and disable (turn off) the rule that allows ICMP (ping) traffic to come in.</p>
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


<p>Return to your Windows 10 VM. Continue observing the ICMP traffic in Wireshark and monitor the command line for any changes in the ping activity.
</p>
<p>  
<img src="https://i.imgur.com/6IkGjgN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>Go back to your Ubuntu VM's Network Security Group settings and turn back on the permission for incoming ICMP traffic.
</p>
<p>
<img src="https://i.imgur.com/hLvCuMG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Return to your Windows 10 VM, monitor the ICMP packets in WireShark, and check the Command Prompt's ping operation, which should now be successfully sending and receiving packets.</p>
<p>
<img src="https://i.imgur.com/xa3wpqq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
End the ongoing ping command by pressing `Ctrl + C` in the Command Prompt window.</p>
<p>
<img src="https://i.imgur.com/5vh29Fb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
In Wireshark, apply a filter to show only SSH traffic by entering `ssh` in the filter bar and pressing Enter.</p>
<p>
<img src="https://i.imgur.com/YVan6HT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
From your Windows 10 virtual machine, use an SSH client to connect to your Ubuntu VM using its private IP address. Pay attention to Wireshark on your Windows VM to observe the network activity during the SSH connection setup, especially when you enter the password to log in to the Ubuntu VM.</p>
<p>
<img src="https://i.imgur.com/BMzNR4K.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>Once you've successfully connected to your Ubuntu VM via SSH, monitor and analyze the network activity displayed in Wireshark to understand what happens during an active SSH session.</p>
<p>
<img src="https://i.imgur.com/nkK8e9P.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>To close the SSH session, simply type `exit` and then press the [Enter] key.</p>
<img src="https://i.imgur.com/a0mufR0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
In Wireshark, apply a filter to display only DHCP traffic by entering "dhcp" in the filter bar.</p>
<p>
<img src="https://i.imgur.com/ikQdqx1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>On your Windows 10 VM, open the Command Prompt and run the command <code>ipconfig /renew</code> to request a new IP address for your machine.</p>
<p>
<img src="https://i.imgur.com/KcW8DrY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
In Wireshark, apply a filter to display only DNS traffic by entering "dns" into the filter bar.</p>
<p>
<img src="https://i.imgur.com/tGO1eSE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>Open the command line on your Windows 10 virtual machine and enter the commands <code>nslookup google.com</code> and <code>nslookup disney.com</code> to find out the IP addresses of google.com and disney.com, respectively.</p>
<p>
<img src="https://i.imgur.com/YMpASho.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>While in Wireshark, watch the DNS traffic to see how the DNS queries for the websites you looked up are displayed.</p>
<p>
<img src="https://i.imgur.com/AZkQiix.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>Return to Wireshark and apply the filter for RDP traffic using <code>tcp.port == 3389</code>. Notice the continuous flood of traffic that appears.</p>
<p>
<img src="https://i.imgur.com/n2m7GY8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>Observe that the RDP protocol maintains a continuous connection, resulting in a steady stream of data transmission between the two computers.</p>
<img src="https://i.imgur.com/yxHKPOd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
<img src="https://i.imgur.com/UDawVdl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


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

- Step 1: In Microsoft Azure portal create a Resource Group. a Windows 10 Virtual Machine and a Linux Ubuntu Virtual Machine. Then open the Windows 10 VM in Remote Desktop.
- Step 2: On the Windows 10 Virtual Machine download, install Wirshark, and open Wireshark to start observing live traffic (a.k.a packets) on the Virtual Machines.
- Step 3: In Wireshark ICMP traffic will be filtered first.
- Step 4: Ping SSH.
- Step 5: Filter for DHCP traffic.
- Step 6: Filter for DNS traffic.
- Step 7: Filter for RDP traffic.

<h2>Actions and Observations</h2>

<p>
<img src="https://docs.google.com/document/d/1yDry7F0Kb_GEfyqvSx1sdIOBdmiNaX3SU7XD0ym9gyI/edit" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the Microsoft Azure portal, I have created a Resource Group, a Windows 10 Virtual Machine and a Linux Ubuntu Virtual Machine. Using Remote Desktop I have opened the Windows 10 VM. Then I downloaded, installed, and opened Wireshark. The live traffic on the Virtual Machines can be observed in the inital opening of Wireshark, as show above. 

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now that I have opened Wireshark I will clear the packets being shown and filter for ICMP traffic only by typing it into the "Apply a display" bar at top.
Next I have retrieved the private IP address of the Ubuntu VM and attempted to ping it from within the Windows 10 VM. The ping requests and replies can be observed within WireShark as shown above. 
                   A. A  perpetual ping from VM1 to VM2 signaling that traffic is getting through it to destination VM2 successfully and on time.
                   B. A successful attempt to ping google.com, 
                   C. You can observe a blocked and unblocked traffic flow of the perpetual ping as I have gone into to the windows 10 VM and disabling then re-                             enabling the incoming(inbound) ICMP traffic

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here I have filtered SSH to observe SSH traffic only. In my Windows 10 VM Powershell, I have entered the SSH command via the Ubuntu VM's private IP address. Followed by entering the Ubuntu VM's username, and password commands into the shell prompts. Now I have connected VM1 to VM2 as you can see the command line has VM2 as the user. So essentially I am now in the Ubuntu Linux VM as shown by the difference in command line name and structure. I can now use different commands to find out information about the computer, network, etc. SSH is also tcp.port = = 22 in Wireshark.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next I have filtered for DHCP traffic. DHCP is used to automatically assign you an IP address, so on this step I will force the renewal of an IP address with DHCP IP configuration and observe the change. We can also see the ip address re-issued to us in powershell.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now I'm going to filter for DNS traffic which means Im going to ask the DNS server what the IP address is for any given server. So from my Windows 10 VM within a command line, I have used nslookup to see what google.com's IP address is. As shown in the picture, Google's IP address has popped up in the command line. DNS in wireshark is also: UDP.port = = 53.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lastly, I have filtered for RDP traffic. We use RDP to interact with the computer.
Once you put in the rdp filter you will see the packets/spam of traffic start to constantly keep loading up. This is different from the other protocols we’ve observed where the packets do not keep loading. This is because the RDP protocol is constantly showing a live stream of traffic being transmitted from one computer to another. RDP in wireshark is also: TCP.port = =3389.
</p>
<br />

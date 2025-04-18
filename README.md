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

- Within your Windows 10 Virtual Machine, Install Wireshark
- Open Wireshark and start packet capture
- Within Wireshark, filter for ICMP traffic only
- Attempt to ping the Ubuntu VM (linux-vm) from within the Windows 10 VM
- Configuring a Firewall [Network Security Group]

<h2>Actions and Observations</h2>

<p>
  
![Screenshot 2025-03-08 200949](https://github.com/user-attachments/assets/e6ce1e21-9d0d-4a20-a44b-9de6f4499df0)


</p>
<p>
I begin the lab by creating two virtual machines in Azure. One Windows10 vm and a linux-vm. They are both in East US 2 region with the same resource group named AnthonyNetworkingActivities as well as the same virtual network. I opened Remote Desktop and copied the windows 10 vm IP Address and pasted in RDP and clicked Connect.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 201926](https://github.com/user-attachments/assets/3707e917-75cf-44b1-b1d0-f70c1dd3e6a9)

</p>
<p>
Once in the Windows10 vm, opened up Microsoft Edge and went to https://www.wireshark.org
</p>
<br />

<p>
  
![Screenshot 2025-03-08 202003](https://github.com/user-attachments/assets/677f3ded-b1e2-4bcd-83ac-50589a978ad7)


</p>
<p>
Go to the download section and select the Windows x64 Installer.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 202055](https://github.com/user-attachments/assets/9f385f9f-8407-410a-b248-d8c01768cfc0)


</p>
<p>
Once the installer appears select next and leave all settings as is.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 202818](https://github.com/user-attachments/assets/f9c50670-5c31-4080-b7bb-9827ff5cac14)


</p>
<p>
Wireshark has been installed successfully. Click finish.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 205902](https://github.com/user-attachments/assets/f021022d-fd20-4680-a03d-5b9a9363a3be)


</p>
<p>
Once Wiresharkk is open, select the Ethernet and click on the shark fin on the top left of the tool bar in order to start capturing the network traffic.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 210237](https://github.com/user-attachments/assets/de8abe18-0e00-4348-a27d-d22fedfc2ce4)

</p>
<p>
The network traffic is being captured.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 210319](https://github.com/user-attachments/assets/fd7a4a99-d605-4115-8e76-eab37ef83b9e)


</p>
<p>
To filter communications only using the ping command, type icmp into the search bar and press enter.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 210338](https://github.com/user-attachments/assets/29cd37e0-f1af-4608-8fa8-2d78d6652a23)


</p>
<p>
Only traffic that uses the ping command is now displayed by Wireshark.
</p>
<br />

![Screenshot 2025-03-08 210638](https://github.com/user-attachments/assets/1e2af61f-3b86-4112-80e1-8fa894deb4a5)


</p>
<p>
Open up Windows Powershell.
</p>
<br />


<p>
  
![Screenshot 2025-03-08 210909](https://github.com/user-attachments/assets/9ec303ef-865e-4185-9837-4d38c0262f61)

</p>
<p>
To make sure it was responding, I attempted to ping the Linux virtual machine using the public IP address 10.0.0.5, and it was successful.  Wireshark displays the communication being pinged to and from the Linux and Windows virtual machines.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 211450](https://github.com/user-attachments/assets/b46e6ba3-d254-4e23-9483-8830d938d035)

</p>
<p>
After that, I used ipconfig /all to see the network configurations and saw that the mac address and physical address in Wireshark match.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 212601](https://github.com/user-attachments/assets/5c5258da-96b6-4135-a5ba-60f382309940)

</p>
<p>
After that, I entered 10.0.0.5 -t to ping continuously.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 212742](https://github.com/user-attachments/assets/0fe55cd5-eac7-4ccd-9864-20b4044396c0)

</p>
<p>
Back in Azure, I selected the linux-vm to enter into the configurations.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 212813](https://github.com/user-attachments/assets/70cbea62-b8a7-4f97-bfd3-7dae57f300cf)

</p>
<p>
Navigate to Networking and Network Settings.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 212923](https://github.com/user-attachments/assets/ecbf0dca-3528-43f8-8a0c-fac1712a5f5a)

</p>
<p>
Click on the Network interface/ IP configuration to enter the settings.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 212950](https://github.com/user-attachments/assets/09fa7df1-2e45-4d58-9ba2-b8104bd845a8)

</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 213002](https://github.com/user-attachments/assets/31dfa520-d490-46d0-ae4c-4b19689d7129)

</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 213139](https://github.com/user-attachments/assets/af24ac8a-e726-4a04-94b7-977b70fca5f0)

</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 213155](https://github.com/user-attachments/assets/82871223-53aa-4594-8900-e47de22c69ce)

</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 213235](https://github.com/user-attachments/assets/e3464bf2-9fed-40fa-8275-50d0b8feb4ae)

</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 213310](https://github.com/user-attachments/assets/09132234-55dd-4395-80ae-3d5ea86835d2)

</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 213532](https://github.com/user-attachments/assets/ea3b6f8b-33ca-4e82-9978-bf8de10bb12f)

</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 213543](https://github.com/user-attachments/assets/5aa0fbe5-8e16-4f4a-bbf3-5159f3025a28)

</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 213552](https://github.com/user-attachments/assets/3996cc1c-e318-4bd3-b7b2-ac3356ebdf5f)

</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
  
![Screenshot 2025-03-08 213657](https://github.com/user-attachments/assets/7ac305e7-9925-4293-841f-69586ecf4337)

</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />


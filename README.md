<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)



<h2>Deployment and Configuration Steps</h2>

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/4ce8b241-a52c-4caa-84e7-7c46ae20b016)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/2d912855-f502-4363-8f8d-cd0436e5d6d5)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/b84d08af-7f5f-42c9-a4fb-3876b90158f1)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/8db8c1b8-af46-481a-b2ee-3ca4ca1ea795)


**1.) First we will create two Virtual Machines in Azure one will be a Domain controller running windows server 2022 and the other a VM running Windows 10 (*make sure to check that they are in the same VNET*)**

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/84324e9f-7c42-4b9e-9113-e2bd72e9d397)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/7e30d960-12b1-409a-9513-5738a15d5746)
**2.) Go to Domain Controller VM and click on Networking and click on Network Interface then after that go to IP config and change the IP address to *Stactic* so it never changes and hit save.**

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/f0227dfd-b7f7-4d64-b821-06ad245fb056)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/63d30a66-4f7c-4bf1-a7dd-b8ca3c1adf33)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/fd3d4d6d-3ca7-47d5-97a2-c5c96618933f)

**3.) Ensure Connectivity between the client VM and Domain Controller by logging in to Client VM and perpetual ping Domain Controllers Private IP which is 10.0.0.4 for me and as you can see it the request times out which shows that the firewall is working inside the domain controller.**

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/1161e8fa-ad87-42f7-9a16-f8b4770c5f4f)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/3238bcbf-7d56-4a48-87f4-6afd590eb7a9)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/d58a05b2-2ac7-4519-a086-b8b9fb328523)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/72781819-b114-4294-99c4-8ea8826f9fa0)

**4.) From here we will now log into Domain controllers VM and change Firewall Permissions to allow ICMP Traffic.**

**So first you go to windows defender firewall and click inbound rules and click protocol and go to ICMPv4 and Enabled both echo request.
Then when you check back into Client VM you can see replys from Domain controller VM now which tells you that there can be connectivity between the Client VM and Domain Controller.**













which will allow us to change the other VM's DNS Server manually into the Domain controller as its DNS Server.



Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.



Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
















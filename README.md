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

















which will allow us to change the other VM's DNS Server manually into the Domain controller as its DNS Server.



Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.



Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
















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


**1.) First we will create two Virtual Machines in Azure one will be a Domain controller VM running windows server 2022 and the other a VM running Windows 10 (*make sure to check that they are in the same VNET*)**

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/84324e9f-7c42-4b9e-9113-e2bd72e9d397)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/7e30d960-12b1-409a-9513-5738a15d5746)
**2.) Go to Domain Controller VM and click on Networking and click on Network Interface then after that go to IP config and change the IP address to *Stactic* so it never changes and hit save.**

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/f0227dfd-b7f7-4d64-b821-06ad245fb056)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/63d30a66-4f7c-4bf1-a7dd-b8ca3c1adf33)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/fd3d4d6d-3ca7-47d5-97a2-c5c96618933f)

**3.) Ensure Connectivity between the client VM and Domain Controller VM by logging in to Client VM and perpetual ping Domain Controllers Private IP which is 10.0.0.4 for me and as you can see it the request times out which shows that the firewall is working inside the domain controllers VM.**

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/1161e8fa-ad87-42f7-9a16-f8b4770c5f4f)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/3238bcbf-7d56-4a48-87f4-6afd590eb7a9)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/d58a05b2-2ac7-4519-a086-b8b9fb328523)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/72781819-b114-4294-99c4-8ea8826f9fa0)

**4.) From here we will now log into Domain controllers VM and change Firewall Permissions to allow ICMP Traffic.**

**So first you go to windows defender firewall and click inbound rules and click protocol and go to ICMPv4 and Enabled both echo request.
Then when you check back into Client VM you can see replys from Domain controller VM now which tells you that there can be connectivity between the Client VM and Domain Controller VM.**

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/225de0ff-a4e9-4787-aa99-cb8831684e2c)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/e74fcf5a-4802-45e6-8079-8a8b848c1587)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/164e95fe-6962-4ba1-83b4-159f0c291b4f)

**5.) Now go back to Domain controller VM and go to server manager and click (add roles and features) and check Active Directory Domain Services and Install. After Installation you will see this pop up and click on *"Promote this server to a Domain Controller"*** 

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/75b3b2e6-8643-42fc-8d37-36df7efaf473)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/6bbcb7d4-53f6-418a-9354-3354b7e40703)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/5ae8fa5c-65a5-4735-97fe-37894babacfc)

**6.) Furthermore, we will add a new forest and make the root domain name in this case I chose mydomain.com then after that we will create a password.
Then once you are ready hit install and the VM will restart and you will have to log in as a *fully qualified domain name* so in this case for me it will be "mydomain.com\labuser" this is because we turned our server into a domain controller.**

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/d36a5a47-0a89-4b9b-8044-f866294739f6)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/d5f05c37-19f0-4ac4-9a1f-d3c9b7a6f60d)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/364defaa-2a02-40ae-9ac9-92705d4917a6)

**7.) Now once your in go to tools and click Active Directory Users and Computers and create a new Organizational Unit called “_EMPLOYEES” and "_ADMINS"**

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/ce4c208c-5f01-4b12-b671-e1d922b10b88)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/5482add3-4bb7-405a-969b-c3e762b35a39)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/f10e7fb3-437a-482f-9d93-973e02f95e79)

**8.) From here we will create a new user in the "_ADMINS" Org unit named "Jane Doe" and create a password for this account then we will make them apart of the domain admins group by right clicking jane and properties, from there we will click "member of" and click "add" which will bring up a box and type "Domain" and click "check names" from there click domain admins and apply. Once Jane has become an admin we can log off Domain Contoller and use Jane Doe from now on.** 


![image](https://github.com/MartindIT/install-config-AD/assets/151476834/1a179523-004a-4d7b-93e4-767621486f74)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/88431288-7b66-42f0-8b74-b39f1866a743)

**9.) At this time we can now log back in as Jane Doe in the Domain Contorllers VM and by typing in command prompt we can see we are logged in as Jane Doe**

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/967416cf-97aa-4885-ab6d-47835c73101c)

**10.) Finally we can go back to our Client VM which has been sitting around and go ahead and go to "System" and "Rename this PC Advanced" and click "change" then type "mydomain.com" into the box and click "ok" and as you can tell it says that mydomain.com can not be contacted which just means it reached out to public DNS Server and not private, From here we will have to change are DNS settings in Azure.**

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/fdb20d74-be19-41c8-b71c-70c323784d3b)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/48b7594f-aaa3-4448-9d69-4ab8a32b45e2)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/5772ece5-55a7-4cd9-8f58-7fbc06a36bf7)

**11.) We will return back to Azure and go to virtual machines to change Client-1's DNS server settings to allow custom dns server from Domain Controller's Private IP Address, Then restart the Client VM to ensure our settings will be changed over and log back in with labuser.**

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/6d38bdda-d521-4147-ab27-aae097c9b0a1)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/38785941-d00c-4a73-8fe2-02c92c92a97d)
![image](https://github.com/MartindIT/install-config-AD/assets/151476834/7b8fd1e5-d324-4c52-86c3-a04ebac1f1fc)

**12.) Once we log back into Client VM we can check our DNS server by command promt and ipconfig /all and it shows what are DNS server is now. Then go to "system settings" and go to "Rename this pc Advanced" and click "change" where you will type "Mydomain.com" and log in as "Jane_admin" then the Client VM wil restart and now since Client VM is a memeber of the domain, we can now log into Jane Doe's account on the Client VM.**

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/8fe669ce-607e-4a82-9c07-33eff76992e4)

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/672703c9-6077-44b0-8ff0-417b901c3eb2)

**13.) Further more just go to settings and go to remote desktop and click "select users who can remotley access this pc" and type "Domain Users" which just allows everyone have access to log into the Client VM, To ensure that this was done you can go back to Domain controller VM and go to Active Directory users and computers and find the users folder in MyDomian.com folder to see all members apart of Domain Users which we'll soon add more.**


![image](https://github.com/MartindIT/install-config-AD/assets/151476834/e30600ac-366e-4349-9656-50e375e9cab0)

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/626382c0-2440-4b2b-9e08-54dc5f7a2d9f)

**14.) Next we will go to Power Shell ISE in the Domain Controller VM as administrator and paste the context of the script into powershell and create a bunch of accounts with random names and to ensure that these are getting transfered to our "EMPLOYEES" org unit we will go into active directory users and computers to watch this unfold. *This script gives everyone the same password so all I have to do now is pick a random one to log in as through Client-1 VM***

![image](https://github.com/MartindIT/install-config-AD/assets/151476834/95e72b15-51ad-412d-8a08-0c12d5ec6ede)

**5.) From here I can log out of Client-1 VM and proceed to log back in as a random user which I Chose "bav.puf"






which will allow us to change the other VM's DNS Server manually into the Domain controller as its DNS Server.



Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.



Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
















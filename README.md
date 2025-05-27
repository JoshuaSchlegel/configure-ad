<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the deployment and setup of Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1) Create a Domain Controller and disable Windows Firewall (to test connectivity)
- Step 2) Create a Client (Virtual Machine) using Windows 10 and confirm connection to the Domain
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
*First we will need to create a Resource Group, Virtual Network and Subnet, and the Domain Controller VM using Windows Server 2022. I will name it DC1 and create the username: labuser and password: Password1234 just to keep things simple.
</p>
<br />

- In Microsoft Azure, type "resource" in the search bar at the top and click on "Resource groups"
- Click the "Create" button either towards top left or the blue one in the middle of the screen.
- I'll name it "ActiveDirectoryLab" and click "Create + Review" -> then click "Create"

![image](https://github.com/user-attachments/assets/d504359a-2c64-459b-82bd-abb7fe7f2c92)

![image](https://github.com/user-attachments/assets/9e74d2f7-b68f-4293-b75f-d1a4c626a880)

![image](https://github.com/user-attachments/assets/0365cc48-65e9-45b3-b0f5-54bd7e61289a)

![image](https://github.com/user-attachments/assets/c083bab4-c009-4e2d-b7d6-5131e22c92d6)

*Next, we'll create our virtual network.
- Type "v" or "virtual network" in the search bar up top and click on "Virtual networks".

![image](https://github.com/user-attachments/assets/ae4c47f4-f1fb-4410-9bb0-31a6d73b2acb)

- Click "create" (just like we did with the resource group).
- Make sure it shows the resource group there, if not click the drop down and select it.
- I'll name the VN (Virtual Network) "ActiveDirectory-VNet". ***(Take note of the region and make sure any Virtual Machines we wind up creating are in that same region.)***
- Click Review + Create and then Create.
- Wait for deployment to complete.

![image](https://github.com/user-attachments/assets/c15aa17c-293e-4f9a-9275-8d231dfa3981)

- Once the VN has been created, type "v" or "virtual machine" in the search bar at the top and click on "Virtual machines"
- Click on "Create" -> Azure Virtual Machine
- Make sure the resource group is the one we created.
- I'll call this VM "DC1".
- Make sure its in the same region as the VN.

![image](https://github.com/user-attachments/assets/40d96467-cfd4-4139-a772-f6870975f944)

![image](https://github.com/user-attachments/assets/1514b29b-775b-4903-8542-831a25a7096d)

- For *Image use "Windows Server 2022 Datacenter: Azure Edition - x64 Gen2"
- For *Size use Standard_D2s_v3 - 2 vcpus, 8 GiB memory    

![image](https://github.com/user-attachments/assets/8485d598-97a2-44d8-ad8e-70f843eadbe4)

- I used username: labuser and password: Password1234
- Once you create your username and password for DC1, click "Next:Disks>" at the bottom and then "Next:Networking>" (the same button)

![image](https://github.com/user-attachments/assets/850fe8b2-27e9-4218-9be1-1d2d2f429a1d)

- Make sure in the Networking tab, it shows the Virtual network we created selected. ***(Sometimes it won't be there which means you need to wait a bit longer before being able to create the Domain Controller VM. In that case just click "home" in the top left and try again until you see the VN show up as an option.)***
- Then click on "Review + Create" -> "Create".

![image](https://github.com/user-attachments/assets/9f19b846-17c2-4885-85e8-8f07a6de5aff)

![image](https://github.com/user-attachments/assets/05fd4ba4-3035-4a4b-8d6f-1cacd4448172)

<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

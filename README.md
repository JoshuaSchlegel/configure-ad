<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the deployment and setup of Active Directory using Windows 11 and Microsoft Azure Virtual Machines. Feel free to try it for yourself at no cost since <a href="https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account">Microsoft Azure</a> can be used with a free subscription for 30 days and/or $200 worth of credits. Lets do it! <br />

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
- Step 2) Create a Client VM (Virtual Machine) using Windows 10 and confirm connection to the Domain
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

**First we will need to create a Resource Group, Virtual Network and Subnet, and the Domain Controller VM using Windows Server 2022. I will name it DC1 and create the username: labuser and password: Password1234 just to keep things simple.**

- In Microsoft Azure, type "resource" in the search bar at the top and click on "Resource groups"
- Click the "Create" button either towards top left or the blue one in the middle of the screen.
- I'll name it "ActiveDirectoryLab" and click "Create + Review" -> then click "Create"

![image](https://github.com/user-attachments/assets/d504359a-2c64-459b-82bd-abb7fe7f2c92)

![image](https://github.com/user-attachments/assets/9e74d2f7-b68f-4293-b75f-d1a4c626a880)

![image](https://github.com/user-attachments/assets/0365cc48-65e9-45b3-b0f5-54bd7e61289a)

![image](https://github.com/user-attachments/assets/c083bab4-c009-4e2d-b7d6-5131e22c92d6)

**Next, we'll create our virtual network.**

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

**Now we need to set the Domain Controller's Network Interface Card's (NIC) to be static instead of dynamic. Then we'll log into the DC1 VM in using Remote Desktop Connection and disable the Windows Firewall.**

- Click "Home" in the top left -> Virtual machine OR type "v" in the search box up top and click "Virtual machine"
- Click on the DC1 VM in the Virtual Machine screen within Azure.

![image](https://github.com/user-attachments/assets/ceb3c5af-d283-4016-adfd-1fd5c4f9286c)

- Click on "Network settings" in the left side panel of DC1.
- (Notice the Private IP address there underlined in green.) Click on the NIC / IP configuration underlined in red.

![image](https://github.com/user-attachments/assets/5a9bd38b-e58e-461e-9795-3b83a2d3c2c8)

- Click on "ipconfig1" towards bottom left of the IP configurations screen.
- Then, click on Static on the right side under Dynamic. (Take note of the Private IP address again here. We'll use that to test connectivity later.)
- Click "Save" on the bottom.

![image](https://github.com/user-attachments/assets/fd44ab47-1007-4c84-8e3d-0dd9837fff0d)

![image](https://github.com/user-attachments/assets/c5202f97-b96e-4fe8-82d8-8755de9a523e)

- Click "Home" in the top left -> Virtual machine OR type "v" in the search box up top and click "Virtual machine"
- Type "remote desktop connection" in the search box in the taskbar and pull up RDC
- Copy/paste the public IP address into the text box in RDC and click "Connect"

![image](https://github.com/user-attachments/assets/03bef0ff-deb1-4b9d-aa49-764348309092)

- Log into the Domain Controller using the Username and Password we created earlier when deploying DC1. (You may need to click on "More choices" on the bottom to change it from the prepopulated username.)
- (Decline any options it presents to you once logged into the Domain.) In the "Search" text box located in the bottom left on the taskbar, type "firewall" and open up Windows Defender Firewall.

![image](https://github.com/user-attachments/assets/cd3e60b3-666c-431f-a1e3-3f6c6463f188)

- Click on "Windows Defender Firewall Properties"

![image](https://github.com/user-attachments/assets/5bc94ea6-3551-4d81-a893-cee1a0932245)

- Across all three of the underlined tabs (Domain Profile, Private Profile, and Public Profile), change the "Firewall state" to Off
- Click "Apply" in the bottom right after all three have been turned off
- Then click "Ok" and close Windows Defender Firewall

![image](https://github.com/user-attachments/assets/b8d9e957-3935-4761-8f25-fa6bb2de073f)

**Next we well need to create the Client VM in Azure (Scroll up to find the steps on where to click to create a VM if you need to see those screenshots again.)**

- Minimize the DC1 VM and go back to Microsoft Azure
- Click on "Virtual machine" under recents on the home screen OR type "v" in the search box up top and click "Virtual machine"
- Click Create -> Azure Virtual Machine
- I will name it "Client1"
- Use Windows 10 Pro 22H2 for *Image
- Use 2 vcpus 8GiB Memory for *Size
- I will set Username: labuser  and  Password: Password1234
- ***Make sure it is in the same region and Virtual Network as DC1***
- Check the Licensing box
- Click "Next: Disks >" and then "Next: Networking >"

![image](https://github.com/user-attachments/assets/00c47443-fce3-47f9-a242-6d156b3c047d)

![image](https://github.com/user-attachments/assets/df49fe0e-1a71-4fd2-8972-bcd740623c31)

![image](https://github.com/user-attachments/assets/63f3018b-5d02-44fe-93f5-928adcd50a65)

- After verifying the VN is the same one we created for DC1, click "Review + Create" and then "Create"

![image](https://github.com/user-attachments/assets/43f6a90d-d6a1-44cf-92e1-c2f8d362ab2a)

**Now we need to set Client1's DNS settings to DC1's Private IP Address. Then, we will ping the Domain Controller to test the connection.**

- After Client1 has been successfully deployed, click on Client1 and go to "Network Settings"
- Click on the Network Interface/IP Configuration (client1559_z1 (primaty)/ ipconfig1 (primary)

![image](https://github.com/user-attachments/assets/0f5700f9-a6b3-4bd1-9689-717143363297)

- Click on "DNS servers" in the left side panel under the "Settings" drop down
- Change the DNS servers from "Inherit from virtual network" to "Custom"
- Type the Private IP address for DC1 in the text box (If you need to see how to find the private IP address for DC1, please scroll back up to find and review the steps.)
- Click Save

![image](https://github.com/user-attachments/assets/6948f03b-ec2d-48f5-9779-36fd221ce15e)

- Go back to the Virtual Machine screen in Azure
- Check the box next to "Client1" and restart Client1 by clicking the 3 dot menu next to "Start"

![image](https://github.com/user-attachments/assets/f5072dda-0c70-4f75-a5da-54edca879c97)

- Once the restart has completed, log into the Client1 VM using Remote Desktop. You'll be able to have multiple Remote Desktops open, so don't worry about still being logged into DC1. Simply pull up another Remote Desktop Connection from the Taskbar Search box. (If you need to see how to log into the Client1 VM using Remote Desktop, please scroll up and review the steps we took to log into DC1.)
- Type "cmd" in the search box on the taskbar and click on "Command Prompt" (Or use "Windows key + R" then type "cmd" -> hit Enter)
- Type "ping (DC1's private IP Address)" and observe the results

![image](https://github.com/user-attachments/assets/583bf8e7-45b5-40e4-a13c-fb3019bf2a5a)

![image](https://github.com/user-attachments/assets/bed00c95-0046-4f74-b200-e3876dd612d8)

**4 Replies show us that the Ping was successful!**

- Type "PowerShell" in the search box on the taskbar
- Open up PowerShell and type "ipconfig /all" and observe the DNS settings showing DC1's private IP Address

![image](https://github.com/user-attachments/assets/9206015d-11d4-423d-ae8d-cc301cfef11e)

![image](https://github.com/user-attachments/assets/52212f0a-a2e3-484e-be60-7c1248e134df)

**Now we are going to install Active Directory Domain Services.**

- Log into DC1 VM usig Remote Desktop (If you need to see how to log into the Client1 VM using Remote Desktop, please scroll up and review the steps we took to log into DC1.)
- In the Server Manager (It should already be started automatically when logging into the Domain) click on "Add roles and features"

![image](https://github.com/user-attachments/assets/128b1523-39c4-4562-9373-7e737072d6eb)

- You'll hit "Next>" 3 times 
- Check the box next to "Active Directory Domain Services" and click "Add Features"
- You'll hit "Next>" 3 more times
- Check the box next to "Restart the destination server automatically if required" and click "yes"
- Click "Install"
- Wait for installation to complete

![image](https://github.com/user-attachments/assets/5964e77d-4a6e-4976-bc54-0ac6efce4195)

![image](https://github.com/user-attachments/assets/3f78e325-7dcb-4aa9-b0b9-3d62053f8378)

![image](https://github.com/user-attachments/assets/03f861b3-f142-4464-9069-dd1cf6c0fe31)

![image](https://github.com/user-attachments/assets/f6749f5d-5961-4f9f-be91-bbb6689d3b19)

![image](https://github.com/user-attachments/assets/8e881d93-d519-4142-adbc-49505a028645)

![image](https://github.com/user-attachments/assets/fca70ada-c8fd-4bb4-9626-d6ebbc229fd3)

- Click "close" once installation completes

![image](https://github.com/user-attachments/assets/452247aa-143d-4df3-bd99-2f169542edc0)

- Click on the Flag icon with the yellow warning triangle by it
- Click "Promote this server to a domain controller

![image](https://github.com/user-attachments/assets/b65c8a7f-6d05-4b68-97c7-7a632462a465)

- Select "Add a new forest"
- Type "mydomain.com" as the Root domain name
- Click "Next>"

![image](https://github.com/user-attachments/assets/a6f24145-6ba6-4b10-8ce6-1d41767f21dc)

- Type "Password1" twice (You'll most likely never use this password)
- Click "Next>" 5 times (You may have to wait a bit on the third "Next" for the BIOS Domain name)
- Click "Install"
- After completion, the VM will be shut down

![image](https://github.com/user-attachments/assets/cfdc056b-4731-40e6-af5b-a830de05d5ba)

![image](https://github.com/user-attachments/assets/8da5d7f6-f9cf-475e-928b-7df5166b3290)

- Log back into DC1 with username: mydomain.com\labuser  and same password you've been using







<p>

</p>
<br />

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

- Creat sample file shares with various permissions
- Attempt to access file shares as a normal user
- Create and test access and permissions for "ACCOUNTANTS" Security Group

<h2>Actions and Observations</h2>

<p>
<b>1.) Create some sample file shares with various permissions</b>
  
- Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)
- Connect/log into Client-1 as a normal user (mydomain\<someuser>)
- On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”
- Set the following permissions (share the folder) for the “Domain Users” group:
- Folder: “read-access”, Group: “Domain Users”, Permission: “Read”
- Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
- Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”
</p>

<p>
<b>2.) Attempt to access file shares as a normal user</b>
  
- On Client-1, navigate to the shared folder (start, run, \\dc-1)
- Try to access the folders you just created. Which folders can you access? Which folders can you create stuff in? Does it make sense?
</p>

<p>
<b>3.) Create an “ACCOUNTANTS” Security Group, assign permissions, an test access</b>
  
- Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”
- On the “accounting” folder you created earlier, set the following permissions:
- Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”
- On Client-1, as  <someuser>, try to access the accountants folder. It should fail. 
- Log out of Client-1 as  <someuser>
- On DC-1, make <someuser> a member of the “ACCOUNTANTS”  Security Group
- Sign back into Client-1 as <someuser> and try to access the “accounting” share in \\DC-1\ - Does it work now?
</p>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


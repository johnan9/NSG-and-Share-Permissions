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

- Windows 10 Pro (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Creat sample file shares with various permissions
- Attempt to access file shares as a normal user
- Create and test access and permissions for "ACCOUNTANTS" Security Group

<h2>Actions and Observations</h2>

<p>
<b>1.) Create some sample file shares with various permissions</b>
  
- Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)
- Connect/log into Client-1 as a normal user (mydomain.com\beji.cur)
- On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”
- Set the following permissions (share the folder) for the “Domain Users” group:
- Folder: “read-access”, Group: “Domain Users”, Permission: “Read”
- Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
- Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”
</p>
<p>
<img src="https://i.imgur.com/A1uBAOy.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/Fy1cGOa.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/Ntrf5N1.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/g5H6KNl.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/KzxXrcS.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/kpht2Su.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>

<p>
<b>2.) Attempt to access file shares as a normal user</b>
  
- On Client-1, navigate to the shared folder (start, run, \\dc-1)
- Try to access the folders you just created. Which folders can you access or not?
  - <b>beji.cur</b> can access <b>Read-access</b> folder but cannot create a folder.
  - <b>beji.cur</b> cannot access <b>No-access</b> folder since he is not a Domain Admin.
</p>
<p>
<img src="https://i.imgur.com/nm0Ut63.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/wkVTuar.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/YdoafSa.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/yKGtVCE.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/wD0ha0R.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>

<p>
<b>3.) Create an “ACCOUNTANTS” Security Group, assign permissions, an test access</b>
  
- Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”
- On the “accounting” folder you created earlier, set the following permissions:
- Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”
- On Client-1, as  <b>beji.cur</b>, try to access the accountants folder. It should fail. 
- Log out of Client-1
- On DC-1, make benji.cur a member of the “ACCOUNTANTS”  Security Group
- Sign back into Client-1 as <b>beji.cur</b> and try to access the “accounting” share in \\DC-1\ - He has access this now.
</p>
<p>
<img src="https://i.imgur.com/0qU4H6s.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/E3C99Hj.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/0rQSjRZ.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/GYq7oSe.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/fxqjfpa.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>


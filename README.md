# File Share Permissions

<p align="center">
<img src="https://i.imgur.com/xlYwPUf.png" height="40%" width="40%" alt="Permissions Photo"/>
</p>

<h1>Objectives</h1>

- Create some sample file shares with various permissions
- Attempt to access file shares as a normal end user / client.
- Create an Accountants Security Group, assign permissions, and test access.

<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (22H2)

<h2>Prerequisites</h2>

  - [Installing and Configuring Active Directory in Azure](https://github.com/ben-trainer/Azure-Active-Directory-Home-Lab)
  - [Understanding DNS in Azure](https://github.com/ben-trainer/dns-testing/tree/main)

<h2>File Permissions Configuration Steps</h2>

<p>
Log in to our DC-1 VM and go to Server Manager > Active Directory Users and Computers > Employees, and select a user to be our client.
</p>

<p>
<img src="https://i.imgur.com/cQNF8HH.png" height="40%" width="40%" alt="Permissions Steps"/>
</p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p>
On the DC-1 VM create a few files to be shared. Open file explorer > This PC > C:, and create folders named: “read access” “write access” “no access” “accounting”
</p>

<p>
<img src="https://i.imgur.com/azoPBZj.png" height="40%" width="40%" alt="Permissions Steps"/>
</p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p>
After the files are created share the files on the domain by right clicking read-access and write access file > Properties > Sharing, type in “domain users” add > share. 
  
  - Assigning the proper permissions based on the file name we set. (read-access, read only, write-access, read and write access)
</p>

<p>
<img src="https://i.imgur.com/gnJvbKa.png" height="40%" width="40%" alt="Permissions Steps"/>
</p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p>
The no-access file we will do the same process but type in “domain admins” add > share
</p>

<p>
<img src="https://i.imgur.com/EjvlgV6.png" height="40%" width="40%" alt="Permissions Steps"/>
</p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p>
Skipping accounting, we will go over to our CLIENT-1 VM and view our new file shares by typing “\\dc-1” hit enter and the folders should appear.
</p>
  
<img src="https://i.imgur.com/mVtlynG.png" height="40%" width="40%" alt="Permissions Steps"/>
</p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p>
Attempt to open the "no access" file from the client side

  - Access should be denied
</p>

<p>
<img src="https://i.imgur.com/itF98ns.png" height="40%" width="40%" alt="Permissions Steps"/>
</p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p>
To further test permissions, In the DC-1 VM create a text file under This PC > C: > read-access. 
  
-  On the CLIENT-1 VM attempt to create a text file within the same read-access file and it should deny access.
</p>

<img src="https://i.imgur.com/kAHU8d9.png" height="40%" width="40%" alt="Permissions Steps"/>
</p>
<p>
Create an accountants security group and provision specific users with access. 
  
  - On our DC-1 VM we will go to Server Manager > Active Directory Users and Computers, right click our domain, create a new resource group (organizational purposes)
  - Within that resource group, create a new group and name it accountants. 
</p>

<p
<img src="https://i.imgur.com/fnbmrN1.png" height="40%" width="40%" alt="Permissions Steps"/>
</p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p>
Within the accountants folder, start sharing the file, type in accountants, and assign Read/Write access and share.
</p>

<img src="https://i.imgur.com/EV9Isww.png" height="40%" width="40%" alt="Permissions Steps"/>

The Demo.waxos account won’t have access to the group so it can be fixed by assigning that account to the accountants group. 

  - Under Server Manager > Active Directory Users and Computers > _SECURITY_GROUPS > Members > Add. Enter the user’s name, check name, and add the user. This should be the result.
<p>
<img src="https://i.imgur.com/LNe3bJb.png" height="40%" width="40%" alt="Permissions Steps"/>
</p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p>
Log off of the CLIENT-1 VM and re sign in using the proper account and domain name before it.
</p>

<p>
<img src="https://i.imgur.com/AVsG159.png" height="40%" width="40%" alt="Permissions Steps"/>
</p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p>
Now within the CLIENT-1 VM while logged into demo.waxos we were able to successfully access and create a text file to add to the file share.
</p>

<img src="https://i.imgur.com/e6TpmM1.png" height="80%" width="80%" alt="Permissions Steps"/>




<h2>Lessons Learned </h2>
In this lab, it helped me learn that creating a file share with Active Directory setup is extremely intuitive, as I have been using Windows for years it is very straightforward and can be quickly learned just by using simple navigation techniques. I ran into small problems provisioning the demo.waxos user because I had an extra space and also forgot to click check names, but I quickly was able to troubleshoot the problem by attempting it again without the space and clicking the proper button before applying.

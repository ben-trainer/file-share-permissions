# file-share-permissions

<p align="center">
<img src="https://i.imgur.com/xlYwPUf.png" alt="Permissions Photo"/>
</p>

<h1>Understanding File Permissions</h1>
This lab will use my previous Active Directory Lab. Here is a brief overview of what will be accomplished in the lab. 

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

<h2>File Permissions Configuration Steps</h2>

To start we will log in to our DC-1 VM and go to Server Manager > Active Directory Users and Computers > Employees, and select a user to be our client.

<p>
<img src="https://i.imgur.com/cQNF8HH.png" height="80%" width="80%" alt="Permissions Steps"/>

On the DC-1 VM we will create a few files to be shared. Open file explorer > This PC > C:, and create folders named: “read access” “write access” “no access” “accounting”
  
<img src="https://i.imgur.com/azoPBZj.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>
<p>
After the files are created we will share the files on the domain by right clicking read-access and write access file > Properties > Sharing, type in “domain users” add > share. Assigning the proper permissions based on the file name we set. (read-access, read only, write-access, read and write access)
</p>
<br />

<p>
<img src="https://i.imgur.com/gnJvbKa.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>
<p>
For our no-access file we will do the same process but type in “domain admins” add > share

<br />

<p>
<img src="https://i.imgur.com/EjvlgV6.png" height="80%" width="80%" alt="Permissions Steps"/>

Skipping accounting, we will go over to our CLIENT-1 VM and view our new file shares by typing “\\dc-1” hit enter and the folders should appear.

  
<img src="https://i.imgur.com/mVtlynG.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>
<p>
When trying to open the no access file from the client side we do not have access.

</p>
<br />

<p>
<img src="https://i.imgur.com/itF98ns.png" height="80%" width="80%" alt="Permissions Steps"/>

To further test our permissions, In our DC-1 VM we will create a text file under This PC > C: > read-access. Then on our CLIENT-1 VM we will attempt to create a text file within the same read-access file and should have our access denied.

<img src="https://i.imgur.com/kAHU8d9.png" height="80%" width="80%" alt="Permissions Steps"/>
</p>
<p>

<br />


Next we will create an accountants security group and provision specific users with access. On our DC-1 VM we will go to Server Manager > Active Directory Users and Computers, right click our domain, create a new resource group (organizational purposes) and within that resource group we will Create a new group and name it accountants. 

<img src="https://i.imgur.com/fnbmrN1.png" height="80%" width="80%" alt="Permissions Steps"/>

Within our accountants folder we can start sharing the file and type in accountants with Read/Write access and share.

<img src="https://i.imgur.com/EV9Isww.png" height="80%" width="80%" alt="Permissions Steps"/>

The Demo.waxos account won’t have access to the group so we will fix that by assigning that account to the accountants group. Under Server Manager > Active Directory Users and Computers > _SECURITY_GROUPS > Members > Add. Enter the user’s name, check name, and add the user. This should be the result.

<img src="https://i.imgur.com/LNe3bJb.png" height="80%" width="80%" alt="Permissions Steps"/>

Next we will log off of the CLIENT-1 VM and re sign in using the proper account and domain name before it.

<img src="https://i.imgur.com/AVsG159.png" height="80%" width="80%" alt="Permissions Steps"/>

Now within the CLIENT-1 VM while logged into demo.waxos we were able to successfully access and create a text file to add to the file share.


<img src="https://i.imgur.com/e6TpmM1.png" height="80%" width="80%" alt="Permissions Steps"/>


<h2>Lessons Learned </h2>
This lab helped me learn that creating a file share with Active Directory setup is extremely intuitive, as I have been using Windows for years it is very straightforward and can be quickly learned just by using simple navigation techniques. I ran into small problems provisioning the demo.waxos user because I had an extra space and also forgot to click check names, but I quickly was able to troubleshoot the problem by attempting it again without the space and clicking the proper button before applying.

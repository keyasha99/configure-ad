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

<h2>High-Level Deployment and Configuration Steps</h2>

- Install Active Directory
- Create a Domain Admin user within the domain
- Join Client-1 to the domain
- Set up Remote Desktop for non-administrative users on Client-1

<h2>Deployment and Configuration Steps</h2>

<h3>Install Active Directory</h3>

<p>
<img src="https://i.imgur.com/rhl2hGX.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Log into the Windows Server. The Server Manager should pop up after logging in. Go to Add roles and features in the Quick Start menu.
</p>
<br />

<p>
<img src="https://i.imgur.com/5kaG9P3.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Click Next.
</p>
<br />

<p>
<img src="https://i.imgur.com/je8lgaK.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Make sure you select Role-based or feature-based installation.
</p>
<br />

<p>
<img src="https://i.imgur.com/JvhkxAd.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
When you get here, check Select a server from the server pool. Your Windows Server should already be highlighted in the box below.
</p>
<br />

<p>
<img src="https://i.imgur.com/RUYKz5i.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
For Server Roles, you are going to select Active Directory Domain Services.
</p>
<br />

<p>
<img src="https://i.imgur.com/tma3hst.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Click Add Features and continue with the installation. 
</p>
<br />

<p>
<img src="https://i.imgur.com/RLvkLOD.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
When you get to Confirm installation selection, check the box for Restart the destination server automatically if required. Click Yes on the pop up window and finish the installation.
</p>
<br />

<p>
<img src="https://i.imgur.com/rtX4kfC.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
After the installation is done, go to the notification flag at the top and click Promote this server to domain controller.
</p>
<br />

<p>
<img src="https://i.imgur.com/A6gaAr0.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Select add a new forest and put mydomain.com for the Root domain name.
</p>
<br />

<p>
<img src="https://i.imgur.com/Ix9xL7s.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Set your password and move on with the next step.
</p>
<br />

<p>
<img src="https://i.imgur.com/WBwUkYl.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Uncheck Create DNS delegation.
</p>
<br />

<p>
<img src="https://i.imgur.com/p9Xufpi.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
This part takes a moment to load, but the NETBIOS domain name should appear. Leave as is and continue.
</p>
<br />

<p>
<img src="https://i.imgur.com/WhB4AhI.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Once the configuration is done, your Windows Server will restart itself. When logging back in to the server, make sure you put mydomain.com/[username] for user. Use the same password as before.
</p>
<br />

<h3>Create a Domain Admin user within the domain</h3>

<p>
<img src="https://i.imgur.com/56ZRlcM.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
After logging back in the Windows Server, open Start and go to Active Directory Users and Computers under the Windows Administrative Tools folder.
</p>
<br />

<p>
<img src="https://i.imgur.com/Uk8kIkl.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Right-click mydomain.com and go to New and then Organizational Unit.
</p>
<br />

<p>
<img src="https://i.imgur.com/bspxcnL.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Name the Organizational Unit "_EMPLOYEES". Create another one and name it "_ADMINS".
</p>
<br />

<p>
<img src="https://i.imgur.com/5O6ixsW.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
In _ADMINS, create a new user.
</p>
<br />

<p>
<img src="https://i.imgur.com/ILyuFqN.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Fill out the names and User logon name. 
</p>
<br />

<p>
<img src="https://i.imgur.com/9NHj9uJ.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
For this tutorial, I checked Password never expires.
</p>
<br />

<p>
<img src="https://i.imgur.com/k85HFWL.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Finish creating the Domain Admin user.
</p>
<br />

<p>
<img src="https://i.imgur.com/lTbOn0b.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Go to Properties for your domain user.
</p>
<br />

<p>
<img src="https://i.imgur.com/gcetiX3.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Go to the Member of tab and click Add to add your user to the Domain Admins group.
</p>
<br />

<p>
<img src="https://i.imgur.com/jZwo7kM.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Type domain admins, click Check Names and then click OK.
</p>
<br />

<p>
<img src="https://i.imgur.com/0SE6IWn.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Click Apply and then OK.
</p>
<br />

<h3>Join Client-1 to the domain</h3>

<p>
<img src="https://i.imgur.com/wyRjBbt.jpeg" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Here, you are going to join your Windows 10 VM to the domain. Login to the VM as your local admin user, right-click the Start menu and go to System.
</p>
<br />

<p>
<img src="https://i.imgur.com/SRujbIT.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Scroll down and go to Rename this PC (advanced).
</p>
<br />

<p>
<img src="https://i.imgur.com/B1PF213.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Click on Change to change the domain.
</p>
<br />

<p>
<img src="https://i.imgur.com/bYim5wJ.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Enter the domain and click OK.
</p>
<br />

<p>
<img src="https://i.imgur.com/4N7xBrM.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
This window will up and you be prompted to enter the username and password of your domain admin.
</p>
<br />

<p>
<img src="https://i.imgur.com/ZhuABYy.jpeg" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
This message will come up after joining the VM to the domain.
</p>
<br />

<p>
<img src="https://i.imgur.com/nPLNaMg.jpeg" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Another message will pop up about restarting the computer to appply the changes.
</p>
<br />

<p>
<img src="https://i.imgur.com/gDFzR00.jpeg" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
When you close all of the programs, you will be asked whether you want to restart the computer now or later. Select Restart Now.
</p>
<br />

<p>
<img src="https://i.imgur.com/CitgsAY.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
When you login back into the Windows Server and go to Active Directory Users and Computers, you will see the Windows 10 computer in the Computers folder. Create a new Organizational Unit, name it "_CLIENTS", and move the computer to _CLIENTS.
</p>
<br />

<h3>Set up Remote Desktop for non-administrative users on Client-1</h3>

<p>
<img src="https://i.imgur.com/o7iJ1q7.jpeg" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
After restarting your Windows computer, log back in as mydomain.com\[username]. Open System Properties.
</p>
<br />

<p>
<img src="https://i.imgur.com/AFyO5si.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Scroll until you see Remote desktop.
</p>
<br />

<p>
<img src="https://i.imgur.com/UoCYdp6.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Go to Select users that can remotely access this PC.
</p>
<br />

<p>
<img src="https://i.imgur.com/jghY3Jj.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Click Add.
</p>
<br />

<p>
<img src="https://i.imgur.com/jyRL2wh.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Enter domain user, go to Check Names, and click OK.
</p>
<br />

<p>
<img src="https://i.imgur.com/YgLJVac.png" height="80%" width="80%" alt="Configure Active Directory"/>
</p>
<p>
Click Add and then OK.
</p>
<br />

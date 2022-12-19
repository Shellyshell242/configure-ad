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

- Step 1: Setup 2 Virtual machines (VM) 
- Step 2: Test the Network between the Client- and Domain Controller (DC-1)
- Step 3: Setup your Domain  
- Step 4: Setup a new User in Active Directory
- Step 5: Join Client-1 to Domain
- Step 6: In Client-1 set up Remote Desktop for Non-Admin Users 


<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/9fpSWLz.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log into Microsoft Azure, Setup the Resource Group, next create the Domian Controller Virtual Machine (VM), select (Windows Server 2022) as the OS and name the (VM) DC-1, switch the DC-1 NIC Private IP address from Dynamic to static. 

</p>
<br />

<p>
<img src="https://i.imgur.com/1dtPChm.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Setup the 2nd  (VM), select (windows 10) for the OS and name it Client-1, keep in mind both (VM’s) must be on the same Virtual Network (Vnet) in order to communicate with each other.

</p>
<br />

<p>
<img src="https://i.imgur.com/BUunpt4.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Use Remote Desktop to log into DC-1, next enable the IMCPv4 permissions in the windows defender firewall Advanced Security settings. Log into Client-1 and ping DC-1 private IP address, if the IMCPv4 was correctly enabled then you should see a reply back from DC-1.


<p>
<img src="https://i.imgur.com/BLguF19.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log in DC-1 and install Active Directory, once Active Directory is installed promote as a DC, select a new forest as mydomain.com (or any name you choose), Once Remote Desktop  restarts log back in as user: mydomain.com\labuser. 
</p>
<br />

<p>
<img src="https://i.imgur.com/JnQ1LqR.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Active Directory Users and Computers create two Organizational Units (OU), on named _ADMINS and the other called _EMPLOYEES.

</p>
<br />

<p>
<img src="https://i.imgur.com/twhgzi7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the _ADMIN (OU) create a new user, once the user is created add the user to the Domain Admins Security Group.
</p>
<br />

<p>
<img src="https://i.imgur.com/UbhhRSI.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/D9RORUv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>  
<img src="https://i.imgur.com/WPcbUuR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Client DNS settings must be changed in Azure Portal to match the Private IP address as DC's Private IP Address, then restart Client. 
In "About Pc" change the Client domain to the same as DC, Create a new (OU) called _Clients, Open systems settings in Client-1, In Remote Desktop allow domain users access to log in Client-1.Log into Client-1 as jane_admin: (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1), copy and upload the script in the link to powershell ISE to generate artifitial employees to use to log into Client-1. 



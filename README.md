# Active_Directory-Oracle_VirtualBox
This is a setup a basic Home Lab Running Active Directory (Oracle VirtualBox) and we will add users using PowerShell.

<h2>Practical Skills Developed</h2>

<b> Active Directory Management | PowerShell | Windows Server | Virtualisation | System administration | Troubleshooting | Security and Access Control | Identity and Access management | Networking | Group Policy Management </b> 

<h2>Tools Used</h2>

- <b>Microsoft Windows 10</b> 
- <b>Microsoft Server 2019</b>
- <b>Powershell</b> 
- <b>Oracle virtualbox</b> 
- <b>Virtual box installation extention pack</b> 

<h2>Environments Used </h2>

- <b>Windows 11</b>

<h2>Process-walk-through:</h2>

<p align="Justify">
  
First I designed an overview of how the whole setup is going to be. This will guide me as to what to do and follow through making sur eI achive all my objectives. So we are going to download and install Oracle virtualBox as well as Windows 10 and Windows Server 2019 on the VM. Additionally download the VirtualBox intallation extention pack which will just help with the VM interface interactions. 
  
We then create a VM which will house the Win Server2019 and domain controller. We will give this VM two Network Interface Cards(NIC), one connects to the internet on our host and the other internally form which other users can connect to like a private network.Then we will istall Server2019 and assign an IP address to the inetrnal network.
  
 Then we will isntall Active Directory Service and cretae a domain. Then we will also install Remote Access Service(RAS) and Network Access Transalation(NAS) so that the clients of the private network can connect to the internet.
  
  Then we will set up a DHCP on the domian controller so that when we set up the Windows10 client it can automatiaclly get IP address from the domain controller.
  
  The we will run a PowerShell script that will automatically create a 1000 users in active directory.
  
  Then we are going to create another VM and install Windows 10 on it which will be connected to the private VM nectwork, we are then going to join it to the domain and log in with one of our created user accounts.
  
  At this point we will be done. I will show most of it with snapshots I took. Appologies I got carried away sometimes and could not take really step by step snapshots but what I have should give a clear representaion of the processes I wentr through.
  
Insatll the Oracle VMBox and ste up a VM <br/>
    
<img src="https://i.imgur.com/Gk4ocYX.png" height="80%" width="100%" /> 
  
<img src="https://i.imgur.com/j7qtzPE.png" height="80%" width="100%" /> 
  
 Set up the Windows Server 2019 and Virtual box installation extention pack and login with the password created.
  
  <img src="https://i.imgur.com/8Hm5X8W.png" height="80%" width="100%" /> 
  <img src="https://i.imgur.com/DFrV3sf.png" height="80%" width="100%" /> 
  <img src="https://i.imgur.com/jjWwH4E.png" height="80%" width="100%" /> 
  
The we will go to the network adapter to configure the internal NIC. In order to identify both we can name it it internet and internal instead of ethernet1 and ethernet2. We will then confiqur the internal IPv4 with the IP details shown in the design. We can omit the default gateway as the domain controller can serve as the defautl gateway.  <br/>
  
<img src="https://i.imgur.com/d26ntXH.png" height="80%" width="100%" /> 
  
So now we are going to create the Active Directory and Domain Service. We go to the service maanager and navigate to the Acitive directory Domain Servie and follow the, read and promts. <br />
  
<img src="https://i.imgur.com/JWPDeze.png" height="80%" width="100%" />
<img src="https://i.imgur.com/9t78or5.png" height="80%" width="100%" />
<img src="https://i.imgur.com/oIGVSvf.png" height="80%" width="100%" />
<img src="https://i.imgur.com/sxzzxKM.png" height="80%" width="100%" />
<img src="https://i.imgur.com/7EIllNo.png" height="80%" width="100%" />
  
You'll notice a yellow flag on the Server Manger, click on that to do a post Deployment Configuration of the ADDS. This is to create the domain itslef. Go through the promts and istall. After restart you will notice the mydomain\... as a prefix to the computer name for login.
<img src="https://i.imgur.com/9llbpw9.png" height="80%" width="100%" />
<img src="https://i.imgur.com/ZlONFrN.png" height="80%" width="100%" />
<img src="https://i.imgur.com/JXskwkQ.png" height="80%" width="100%" />
<img src="https://i.imgur.com/gRffyj9.png" height="80%" width="100%" />

Now we are goint to create make our own administrator instead of the one given during installation.
Go to Active Directory Users and Computers, craete a group or organisation aclled 'Admins'. Create a user in the group 'Admins' Afterwards make the user a member of the domain admins. Log out and log in again with the your admin account.

<img src="https://i.imgur.com/A6XzGpt.png" height="80%" width="100%" />
<img src="https://i.imgur.com/mrBULUo.png" height="80%" width="100%" />
<img src="https://i.imgur.com/zGVYuGT.png" height="80%" width="100%" />
<img src="https://i.imgur.com/f5fdEKQ.png" height="80%" width="100%" />
<img src="https://i.imgur.com/qdy1J0r.png" height="80%" width="100%" />
  
The next step is to create the RAS/NAT to allow the Win 10 to be on the private access network but still be able to access the internet through the domain controller. As usual go to the Server Manager, Add roles and features, select Remote Access and then Routing and then next to install.
  
  The tools and Routing and Remote Access. Then configure and enable and then select Network Address Translation and then select use this interface to connect to the internet and select the 'internt' network and next to finish.

<img src="https://i.imgur.com/Mj3h2SY.png" height="80%" width="100%" />
<img src="https://i.imgur.com/VQXuEoG.png" height="80%" width="100%" />
<img src="https://i.imgur.com/FSDdtA5.png" height="80%" width="100%" />
<img src="https://i.imgur.com/UTQ4fLN.png" height="80%" width="100%" />
<img src="https://i.imgur.com/1EkW7oQ.png" height="80%" width="100%" />
  
  Next we set up a DHCP server to let the Win 10 clients get IP to browse the internet.
  We follow the same process of Add roles and features and install the to tools after installation to set up DHCP scope.

<img src="https://i.imgur.com/RHyEHhA.png" height="80%" width="100%" />
<img src="https://i.imgur.com/mWYnPYQ.png" height="80%" width="100%" />
<img src="https://i.imgur.com/h6oTlgf.png" height="80%" width="100%" />
<img src="https://i.imgur.com/CKRU0RN.png" height="80%" width="100%" />
  
  Next we are going to create multiple users using a PowerShell scripts. Disclaimer: The sript was acquired for this purpose. Upload the script, enable excution policy to unrestristed cos its our lad and run. Going back to the AD users and computers you will notice the list of all created users.
  
<img src="https://i.imgur.com/a6u4gXF.png" height="80%" width="100%" />
<img src="https://i.imgur.com/bKxZQH3.png" height="80%" width="100%" />
<img src="https://i.imgur.com/BroZ2xg.png" height="80%" width="100%" />
  
  Now we will create another VM and isnstall the Windows 10 going through the basic prompts and processess. And then join the Windows10 to the AD domain. Then we will use a random user accounts to log into the PC1 computer(eg. rloveless).
    
<img src="https://i.imgur.com/2X2qBw9.png" height="80%" width="100%" />
<img src="https://i.imgur.com/Xtk2sjT.png" height="80%" width="100%" />
<img src="https://i.imgur.com/3yRSNX0.png" height="80%" width="100%" />
<img src="https://i.imgur.com/idhn7Xn.png" height="80%" width="100%" />


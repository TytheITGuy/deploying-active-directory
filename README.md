<p align="center">
<img src="https://i.imgur.com/aMMGyHQ.jpeg" height="80%" width="80%" alt="Setting Up in Azure"/>
<br />

<h1>Deploying Active Directory in Azure</h1>

<h2>Description</h2>
For this portion of the Active Directory project, I install Active Directory on the domain controller, create a domain admin, and join the client VM to the domain.  <br/>
<br />

This project is a continuation of [Active Directory: Preparing Infrastructure In Azure](https://github.com/TytheITGuy/infrastructure-in-azure), so this project picks up where I left off. <br />
<br />

<h2>Environments and Utilities Used</h2>

- <b>Microsoft Azure</b>
- <b>Virtual Machines</b>
- <b>Remote Desktop Connection</b>
- <b>Active Directory</b>

<h2>Operating Systems Used </h2>

- <b>Windows Server </b>
- <b>Windows 10</b>

<h2>Project Walk-through:</h2>

<p align="center">
To start, in the DC (Domain Controller), bring up the Server Manager dashboard, if it's not up already: 

![1- Log into Dc 1](https://github.com/user-attachments/assets/92e206ef-acf5-4424-be2f-d10a0d14bfaa)

 <p align="center">
Here, click on "Add roles and features" > Next > Next > For server selection there should only be one to select: 

![2- Add Roles and Features](https://github.com/user-attachments/assets/2ceb9cc7-cd46-461a-86e8-8b1926268035)

<p align="center">
Now, check "Active Directory Domain Services" > Click "Add Features":  

![3- Adding Active Directory](https://github.com/user-attachments/assets/c2440fd2-1489-4101-aebd-d0411664de13)

<p align="center">
Select "Active Directory Domain Services" > Next > Next > Next > Now select "Restart the destination server automatically if required" and click "Install": 

![4- Active directory installing](https://github.com/user-attachments/assets/0a037dfc-f6a5-4722-be91-a320ac2011b0)

<p align="center">
Next, I have to promote this machine as a DC by configuring it as a new forest as "mydomain.com" (this can be anything, mydomain.com is just easy to remember) So, to do this, I will click on the flag icon with the caution symbol, near the top-right of the Server Manager Dashboard and select "Promote this server to a domain controller":  

![5-setting up a forest](https://github.com/user-attachments/assets/a4edd960-5f71-4a32-a1b0-108fa6c79d4f)

<p align="center">
Then select "Add new forest" and in "Root domain name" I'll type "mydomain.com". Then "Next":  

![6- adding a new forest](https://github.com/user-attachments/assets/d92f1548-728a-4df5-a0a2-f7e325bcb89f)

<p align="center">
 On this screen, click "Install". The machine will restart after the installation: 

![7- adding a new forest part 2](https://github.com/user-attachments/assets/879a444b-2857-4c2b-9143-e03967707783)

<p align="center">
Now, we'll create an admin user. To do this, in the start search bar, search for "Active Directory Users and Computers": 

![8- AD Users and Computers](https://github.com/user-attachments/assets/59f62724-87e7-42c6-8601-51bbe3440027)

<p align="center">
Right click on "mydomain.com" and select "New" > "Organizational Unit" and name it EXACTLY "_EMPLOYEES" (In a future project we will run a script that uses this name to work). Do the same steps here to create an OU (Organizational Unit) named "_ADMINS":  

![9- Creating Employees](https://github.com/user-attachments/assets/5e71f2c5-db39-4fe1-983d-d35f8b5a7a94)

![10- Creating Admins](https://github.com/user-attachments/assets/74916ee7-1ef1-41bc-b7bf-96fef6adb9cb)


<p align="center">
Next, create a new user in "_ADMINS" by right-clicking on "_ADMINS" > New > User and fill it out like so Jane is under admins: 

![11- Jane the Admin](https://github.com/user-attachments/assets/88eac330-cf4d-4abd-8733-beb6f39106a8)

<p align="center">
Jane Doe is now apart of the "_ADMINS" OU, but isn't actually an admin. To make her an admin right-click on her name > Properties > Member Of > Add... > Enter "domain admins" > Check Names > OK > Apply > OK:  

![12- Jane Dor Properties](https://github.com/user-attachments/assets/560f7d8f-4f69-4680-820d-9071dd53ff9a)

<p align="center">
Log back into client-1.  Here I'll join this client to the domain by right-clicking the start menu > Systems > Rename this PC (advanced) > Change > Select "Domain" and enter "mydomain.com" and hit "OK":  

![15- Adding Client 1 to the domain](https://github.com/user-attachments/assets/3b95f1d6-836e-421f-9109-5e128e4ebd89)

<p align="center">
After the restart due to adding client-1, check in the DC machine start seach bar, search for "Active Directory Users and Computers" > mydomain.com > Computers > client-1 should be listed:  

![17- Verifying Client 1 in domain](https://github.com/user-attachments/assets/9cb8329f-2bd1-4f50-b045-3b667877b741)

<p align="center">
Now we can create another OU as we did before and name it "_CLIENTS". Then drag and drop client-1 from "computers" to "_CLIENTS": 

![18- Creating Clients OU](https://github.com/user-attachments/assets/dfffaed0-ff53-4b80-ae54-5a2695227ce4)


<h2>Active Directory is Deployed and Ready for Use! </h2>

<b>We've successfully installed AD on the domain controller, created a domain admin, and joined the client VM to the domain. Next, we'll create users in Powershell by running a script, and then manage the accounts and group policy!  </b>
<br />
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>

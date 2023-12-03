<p align="center">
<img src="https://i.imgur.com/AeiqMDZ.png" alt="Traffic Examination"/>
</p>

<h1>Network-File-Shares-and-Permissions</h1>

In this tutorial, we will be setting up shared network folders & permissions. We will be using our two virtual machines we used in the previous two labs, [here](https://www.github.com/anbere/configure-ad/) is where we started. We will create folders
in the DC-1 Virtual Machine and share them on the network with different permission settings. Only designated people will be able to access/read/write certain files and folders.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Domain Controller/Client Machine)
- Remote Desktop
- Shared Network Files

<h2>Operating Systems Used </h2>

- Windows 10</b>

</p>
<p>
  First we will connect to our two Virtual Machines running in Azure. Login to DC-1 as jane_admin, and login to Client-1 as one of the non administrative users we created in the previous lab. In DC-1, open the file explorer and navigate to the C Drive. Create four new folders named:

   - 'read-access'
   - 'write-access'
   - 'no-access'
   - 'accounting'
  
  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/7a478adc-fb33-46b4-b81b-62920fd6b521)

  Starting with the 'read-access' folder, right click it and select Properties -> Sharing Tab -> Click on Share -> in the textbox type 'domain users' and click Add. Notice the permission level is set to Read by default which is what we want for this folder. Finally click Share.

  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/37b444fc-b71c-4d03-8c70-4ca62f96dd5a)

  Then get to the same Share properties for the 'write-access' folder but before adding Domain Users, change the permission settings to `Read/Write` and then click Share.

  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/2a86c8f2-e96d-45e8-8c46-1700f4bda61b)

  Now for the 'no-access' folder, we will again get to the Share settings and this time we are going to share the folder with 'Domain Admins' rather than Domain Users. This will make the folder a network folder, but only give access to domain admins.

  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/7df99b71-a3e5-4cba-8145-5a142cc1640d)

  Note that after the sharing was completed for each of the folders, the network filepath is given to us for that folder. In this case it is `\\DC-1\no-access`

  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/b95c9944-9b62-40c6-babb-85784f456590)


  Next, switch to the Client-1 machine and were going to navigate to the network folders to test the permissions. Remember Client-1 is logged in as a normal user. In Client-1 open file explorer and type the following folder path: '\\DC-1'. This will open up the location of the folders we just added.
  
  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/4149e65a-cbf4-4ecc-864c-ef5eaeba6f5f)

  
</p>
<br />

<p>
  
</p>
<p>

</p>
<br />

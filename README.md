<p align="center">
<img src="https://i.imgur.com/AeiqMDZ.png" alt="Traffic Examination"/>
</p>

<h1>Network File Shares and Permissions</h1>

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

  Now for the 'no-access' folder, we will again get to the Share settings and this time we are going to share the folder with 'Domain Admins' rather than Domain Users. This will make the folder a network folder, but only give access to domain admins. Hold off on the accounting folder for now.

  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/7df99b71-a3e5-4cba-8145-5a142cc1640d)

  Note that after the sharing was completed for each of the folders, the network filepath is given to us for that folder. In this case it is `\\DC-1\no-access`. 

  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/b95c9944-9b62-40c6-babb-85784f456590)

  Next, switch to the Client-1 machine and were going to navigate to the network folders to test the permissions. Remember Client-1 is logged in as a normal user. In Client-1 open file explorer and type the following folder path: '\\DC-1'. This will open up the location of the folders we just added.
  
  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/4149e65a-cbf4-4ecc-864c-ef5eaeba6f5f)

  If we try to open the `no-access` folder, we are denied access, we configured this correctly.

  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/029e288d-dd59-495f-9ca9-ab2c5ddf9553)

  We will be able to open both the `read-access` and `write-access` folders however we will only be able to edit/create files in the write access folder, we can verify this by trying to create a file in the empty `write-access` folder.

  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/3c8989fd-3f7c-4d6a-a0e5-1cba365cd5de) | ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/a3475c6c-bae6-4a07-a4de-c07dc833f26b)
  |:---:|:---:|

  Now to create our own security group, go back to DC-1 and open `Active Directory Users and Computers`. Right click our domain and create a new Organizational Unit named `_SECURITY_GROUPS`, within that OU, right click and Create New -> Group and name it ACCOUNTANTS.
  
  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/bf511459-0956-45bc-9d6c-ac4b9ef79269)

  Open our file explorer again and get to the Share properties of our accounting folder. This time we are going to add the ACCOUNTANTS security group we just created.

  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/04733081-91c9-4802-93a7-2d1c35d9c27a)

  To test this permission, we are going to choose another employee in our Active Directory and make them a member of the ACCOUNTANTS security group. Choose any employee then Right click -> Properties -> `Member Of` tab -> Click `Add` -> type 'ACCOUNTANTS' -> click `Check Names` -> Click OK and apply.

  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/090afecf-4cf0-411b-8ef5-215b8a6e1ac5)

  First we will try to access the accounting folder from the currently logged in user in Client-1 and we will see we are denied access because this user is not in the ACCOUNTING security group.

  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/2bec2e68-35a2-4f22-8ea7-30034f0aa700)

  Now logout of this user and login as the user we just added to the ACCOUNTANTS security group.

  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/35d0a9fb-a38e-48c1-b472-b98959512013)

  We can access the accounting folder from this user as well as write new files.

  ![image](https://github.com/anbere/network-fileshare-permissions/assets/90169033/54842106-3699-4eca-9b43-2cb36fb08ec3)

  Congratulations, you have completed and learned the basics of Network File Shares and Permissions!
  
</p>
<br />

















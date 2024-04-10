<p align="center">
  
![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/6f80d440-8ee0-46f9-94bf-93f74f1cfb00)
</p>

<h1>Assigning File Permissions in Azure Virtual Machines</h1>
In this tutorial, we will practice setting up different file permissions and access (on a domain) for different users within different groups. This is all done within Active Directory on our Client Virtual Machine in Azure. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory
- File Permissions
- Security Groups

<h2>Operating Systems Used </h2>

- Windows 10 (22H2)

<h2>High-Level Steps</h2>

- Step 1: Create File Shares & Set Permissions
- Step 2: Access File Shares and Test Permissions 
- Step 3: Create Security Group & Grant Additional Permissions
- Step 4: Test Security Group Members' Access

<h2>Actions and Observations</h2>

Step 1: Create File Shares & Set Permissions
- Connect and log into DC-1 as your domain admin account using remote desktop, then connect and log into Client-1 as a normal user using another remote desktop
- In DC-1, go to the start menu and type C:\ and open it, within the C:\drive, create 4 folders with the names "read-access", "write-access", "no-access", and "accounting"

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/74e766d2-1cd7-47bb-b04b-d400d75c5cec)

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/ab970cb2-b624-4087-ace1-743e4984a817)

- Right click on the "read-access" folder and click properties, click the sharing tab and click share, in the bar type "Domain Users" and set the permission to "read", then click share  

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/4dfb4879-0e18-4c14-9f8a-573293619844)

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/69ea2184-c858-4a1a-99d6-c01f716fa5b4)

- In the "write-access" folder, do the same steps but set the permission of the "Domain User" to "Read/Write", then click share

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/53f01ff0-5cac-4bf7-967a-6c69fea15f1d)

-In the "no-access" folder, follow the steps but in the bar, type "Domain Admins" and set the permission "Read/Write", then click share, we will skip the "accounting" folder we created for now   

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/d4871b75-5950-458f-8fb5-2273434c1800)



Step 2: Access File Shares and Test Permissions
-  On Client-1, navigate the the shared folders we created using the start manu and typing \\dc-1 in the bar

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/829d4c0b-4a82-4314-b794-23053b14f26d)

- Try to access the 3 folders we had created and set up permissions for starting with "read-access"

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/042e0a3d-ebf9-4891-abf4-51d76e1a695b)

- "write-access"

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/03455421-5bc9-4a1f-b4c6-6111685262c8)

- "no-access", observe that we cannot access this folder because we had set the permisson of this folder that only Domain Admins can access, as we are in Client-1 as a Domain user, we cannot access this file

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/fa6f161b-f056-4c72-aa26-b1056e5e76df)



Step 3: Create Security Group & Grant Additional Permissions
- In DC-1, open Active Directory Users and Computers, create a organizational unit called "_SECURITY_GROUPS", right click the folder and click new group called "ACCOUNTANTS"

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/5d9be00a-6808-479b-afaf-7b957b9f1107)

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/cb1e8294-2b55-4ec5-829f-8ff940a48311)

-In the "accounting" folder you had created earlier, add the group "ACCOUNTANTS" and set the permissions to "read/write", then click share

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/6aa58360-f115-4c0f-843b-03cdd0b5ff2e)


Step 4: Test Security Group Members' Access
-In Client-1, try to access the "accounting folder" it should give you an error, after, log out of the Client-1 computer

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/0901a08b-a560-4a31-b1ad-155b79cfd410)

-In DC-1, open the in Active Directory Users and Computers application and find the _SECURITY_GROUPS folder we had created, right click on the ACCOUNTANTS group and click properties, in the members tab, click add and add the employee's name then click ok, apply, then ok  

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/f71c2ef2-fbfc-4a53-93b4-b73bc49a1a26)

![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/2b81f1f1-2e04-415a-b4e2-3ff66bca81ec)

- Log into Client-1 as the employee you had added to the ACCOUNTANTS security group and see if you can access the accountinng folder we had created, observe that you have access to this folder 

 ![image](https://github.com/thechristinaq/Network-File-Shares-and-Permissions/assets/165831241/beed383d-8b95-480d-ad84-a620e97c81ae)




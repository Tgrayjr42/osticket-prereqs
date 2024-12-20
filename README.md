# osticket-prereqs
<img src="blob:chrome-untrusted://media-app/a8127fb7-b7db-4196-a817-5d060ecd951a" alt=""/>![image](https://github.com/user-attachments/assets/598ee8f9-df2e-4615-8a2f-90df0b6ba948)

This guide outlines the steps to install and configure osTicket, an open-source help desk ticketing system, on a Windows 10 virtual machine (VM) using Microsoft Azure, IIS, and PHP.

Prerequisites: 

•Microsoft Azure (for creating a VM)

•Internet Information Services (IIS)

•PHP Manager for IIS

•Rewrite Module for IIS

•VC Redist (for PHP dependencies)

•MySQL 5.5.62

•HeidiSQL (for MySQL management)

•osTicket v1.15.8

•You can download the required files from this here (https://drive.google.com/drive/u/0/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6)

Installation Steps


1 Create a Virtual Machine on Azure


•Visit Azure Portal and create a VM with Windows 10 Pro (version 22H2), 2 vCPUs, and 16GB RAM.


 •Once the VM is set up, connect to it using the Remote Desktop Connection app and the public IP address of the VM.

 
 
 ![image](https://github.com/user-attachments/assets/1d18f4ba-153d-4e4a-8e1d-7664af3ab9db)

 ![image](https://github.com/user-attachments/assets/172cc822-b106-4d49-abee-8ab620440140)

 2. Enable IIS (Internet Information Services)

• On the VM, go to Control Panel > Programs > Turn Windows features on or off.


![image](https://github.com/user-attachments/assets/53784a68-c7a3-40e2-9ca1-3f4b7c57d429)

![image](https://github.com/user-attachments/assets/6ea37f07-7d86-4b39-b0d3-8bc23b4c99ac)

•Enable IIS along with CGI and Common HTTP Features under Application Development Features.

![image](https://github.com/user-attachments/assets/bfb7d8b0-5109-4ce7-a954-7a2c30fa359b)

![image](https://github.com/user-attachments/assets/da03b919-4aed-4bf2-bc00-55d040b40db1)

•Verify IIS installation by navigating to http://127.0.0.1 in your browser.

![image](https://github.com/user-attachments/assets/2d6f0e40-bb7c-44ce-a7ba-62ccc223addf)

note: should look like the picture above 

3. Install PHP Manager for IIS

•Download and install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi).

•Then, install the Rewrite Module (rewrite_amd64_en-US.msi).

4. Install PHP

•Create a folder called PHP in the C: drive.

•Download PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x866.zip) and extract it to C:\PHP.

•Install VC_redist.x86.exe to set up required Visual C++ Redistributables.

if this appears always keep file 

![image](https://github.com/user-attachments/assets/b287a0c2-64df-4f81-8f3e-850e05a0aef0)

5. Install MySQL

•Download and install MySQL 5.5.62 (mysql-5.5.62-win32.msi).

•During the setup, select Typical Setup and Standard Configuration.

•Set the root password to Password1.

![image](https://github.com/user-attachments/assets/1e9bf5b2-03ae-4f70-8a12-7ca3888e850f)

hit execute

![image](https://github.com/user-attachments/assets/972a2572-8988-4b10-b24a-09cf9afe8f21)

6. Register PHP with IIS

•Open IIS Manager and navigate to PHP Manager.

![image](https://github.com/user-attachments/assets/6c1f9b93-742d-4fff-ba68-c1995466a626)

•Register PHP by pointing to the php-cgi.exe located in C:\PHP.

![image](https://github.com/user-attachments/assets/4b507d82-6214-46c1-9236-a343e6da7b6e)

•Restart IIS to apply the changes.

![image](https://github.com/user-attachments/assets/1da52018-143e-440e-95e8-14938e36ef24)

7. Install osTicket

•Download osTicket v1.15.8 and extract the upload folder to C:\inetpub\wwwroot.

•Rename the upload folder to osTicket.

•Reload IIS.

![image](https://github.com/user-attachments/assets/6b8f8079-f31f-4931-b6bd-07ad8a2899d2)

8. Enable PHP Extensions in IIS

In IIS Manager, go to PHP Manager and enable the following extensions:

![image](https://github.com/user-attachments/assets/45cd6d93-a3a0-4413-98c2-fe3abbbfd54d)

![image](https://github.com/user-attachments/assets/27208a06-82c7-4f08-922c-a8f6506eeb27)

we want these three extensions 

php_imap.dll

php_intl.dll

php_opcache.dll

![image](https://github.com/user-attachments/assets/b81069d3-3b11-406a-80df-0979c91c51a2)

9. Rename osTicket Configuration File
   
•Navigate to C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php and rename it to ost-config.php.

•Set appropriate permissions:

•Right-click on the file > Properties > Security > Advanced.

![image](https://github.com/user-attachments/assets/35cd7490-b250-472a-9173-5fcbb94ce2be)

•Disable inheritance and remove inherited permissions.

•Add a new Everyone principal with Full Control.

![image](https://github.com/user-attachments/assets/42c95180-94e1-41d0-b3cf-dc90edaa3768)

![image](https://github.com/user-attachments/assets/dee81f43-8ff3-4a77-a110-fc0ea4fe8049)

10. Set Up the MySQL Database

•Open HeidiSQL and create a new session using the following credentials:

![image](https://github.com/user-attachments/assets/c47f63f4-40d6-4727-bc9e-b0ad7787278c)

•Username: root

•Password: Password1

•After connecting, create a new database named osTicket.

![image](https://github.com/user-attachments/assets/ba465024-fb69-4bb5-812a-0c0b3d3f345b)

•In the osTicket installation wizard, enter osTicket as the Database Name, root as Username, and Password1 as Password

11. Clean Up

•After installation, delete the setup folder located at C:\inetpub\wwwroot\osTicket\setup.

•Set the ost-config.php file to read-only.

12. Complete the Installation

•Finish the osTicket setup by accessing the installation page in your browser.

•After completing the setup, you can now log in to your osTicket help desk system.

![image](https://github.com/user-attachments/assets/95108de5-4118-459c-aa2c-bca91c0aca40)

Congratulations!

•You have successfully installed and set up osTicket on your Azure virtual machine with IIS and MySQL. You can now start managing your support tickets using this open-source ticketing system.



























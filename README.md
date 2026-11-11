<h1>On-Premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within two Azure virtual machines.<br/>


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 11 (21H2)
- Windows 11 Home (Host Machine)



<h2>Deployment and Configuration Processs</h2

To begin, log into DC-1 and open Server Manager. Select "Add Roles and Features" from the dashboard.

<img width="1277" height="657" alt="image" src="https://github.com/user-attachments/assets/70e196f9-7aa1-4e31-a63c-2848b6b71562" />

Select "Active Directory Domain Services (AD DS)" under Server Roles and continue through the installation wizard

<img width="820" height="579" alt="image" src="https://github.com/user-attachments/assets/2d46112b-056e-4ca8-96ca-0abd9d5c3b66" />

Continue through the installation wizard. Under Confirmation, select Install to begin installing Active Directory Domain Services.

<img width="619" height="442" alt="image" src="https://github.com/user-attachments/assets/56ade1ab-a53a-4cef-a59c-22167c7645ba" />  <img width="637" height="460" alt="image" src="https://github.com/user-attachments/assets/7c99f54c-ed81-48fc-9473-8bcfe7429d30" />

After installing Active Directory Domain Services, return to Server Manager and select "Promote this server to a Domain Controller" from the notifications menu.

<img width="627" height="413" alt="image" src="https://github.com/user-attachments/assets/45c1196d-ef54-48c3-94e3-fa371c23e0b5" />

In the Configuration Wizard, select "Add a new forest" and enter "mydomain.com" as the root domain name

<img width="620" height="456" alt="image" src="https://github.com/user-attachments/assets/e89114cb-8027-48af-b6c1-9edb66038d40" />

Configure the Directory Services Restore Mode (DSRM) password and continue through the
wizard. Leave DNS delegation unchecked and verify the NetBIOS name.

<img width="622" height="466" alt="image" src="https://github.com/user-attachments/assets/2cf88da2-87a2-4f1e-a56b-3d3bd512ebb3" />

Continue through the remaining configuration screens. Once the prerequisite checks are complete, select Install.

<img width="622" height="458" alt="image" src="https://github.com/user-attachments/assets/d87acad3-d0e0-420b-bc40-1162333c76fa" />

After installation, DC-1 will restart to complete the Domain Controller promotion. Log back in using the domain credentials.

<img width="409" height="446" alt="image" src="https://github.com/user-attachments/assets/81a99941-46e4-4f65-8e82-5720d3b5e4e1" />




Open Active Directory Users and Computers (ADUC) on DC-1. Right-click the mydomain.com domain, select New, and create two Organizational Units (OUs) named "_EMPLOYEES" and "_ADMINS."

<img width="415" height="354" alt="image" src="https://github.com/user-attachments/assets/a2145ac3-ebe8-4b48-ab0b-3eb6fddfd575" /> <img width="433" height="372" alt="image" src="https://github.com/user-attachments/assets/20f5a070-c9c9-4493-9011-2f7694343ce1" />

Inside the _ADMINS OU, create a new user named Jane Doe with the username "jane_admin"

<img width="443" height="366" alt="image" src="https://github.com/user-attachments/assets/840cf013-ca4a-43d8-b218-e3eeca3c9967" />
<img width="434" height="371" alt="image" src="https://github.com/user-attachments/assets/7ee8e854-811c-4403-ba83-80f2973d64ab" />



After creating the account, open its Properties and navigate to the "Member Of" tab. Select Add and add the account to the Domain Admins security group.

Log out of DC-1 and log back in using the new administrative account: mydomain.com\jane_admin.

Verify the account by running whoami in Command Prompt.

<img width="614" height="412" alt="image" src="https://github.com/user-attachments/assets/48602930-d521-444d-bbfc-89a05e1743ba" />

When prompted, enter the domain administrator credentials to authorize the domain join.

<img width="387" height="314" alt="image" src="https://github.com/user-attachments/assets/305fb945-11eb-4c7a-979a-6183ad9db4ed" />


Log into Client-1 using the original local administrator account, labuser. Open System Settings and navigate to the computer name and domain settings. Select Change, choose Domain, and enter mydomain.com.

<img width="448" height="442" alt="image" src="https://github.com/user-attachments/assets/1c6f5728-9f01-4494-a2f6-f95ed93dc591" />

Once the confirmation message appears, restart Client-1.

<img width="300" height="151" alt="image" src="https://github.com/user-attachments/assets/ec926375-12ea-4ddc-86a5-7686b9a8f915" />

On DC-1, open Active Directory Users and Computers and verify that Client-1 appears in the Computers container.

Create a new Organizational Unit named _CLIENTS and move Client-1 into it.

<img width="621" height="429" alt="image" src="https://github.com/user-attachments/assets/f9186ddb-7135-4258-8b72-c700ddd6b0f0" />


Finally, log into Client-1 using the domain administrator account to verify successful domain
authentication.

<img width="465" height="510" alt="image" src="https://github.com/user-attachments/assets/d0421186-03f7-4373-9a10-6221e37bfc2d" />

Log into Client-1 using the domain administrator account, mydomain.com\jane_admin.

Open System Settings and navigate to Remote Desktop.

<img width="620" height="471" alt="image" src="https://github.com/user-attachments/assets/38a59ccb-e53c-4d5a-b449-c0f02890a587" />

Select Remote Desktop Users and click Add

<img width="376" height="333" alt="image" src="https://github.com/user-attachments/assets/18b629f9-ae4b-4813-a4f0-c260ae5d7648" />

Enter Domain Users and confirm the selection

<img width="463" height="274" alt="image" src="https://github.com/user-attachments/assets/79a9752c-4da9-45fb-bd1d-aaa47c5b589b" />

Domain Users have now been added to the Remote Desktop Users group, allowing standard domain accounts to remotely access Client-1, subject to the computer's other access and security settings.


This step uses a PowerShell script (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) to automate the creation of additional Active Directory user accounts. 

On DC-1, open PowerShell ISE as an administrator.

<img width="624" height="314" alt="image" src="https://github.com/user-attachments/assets/38ff07cc-4108-485e-b174-bfa85910ce0e" />

Create a new script, paste the provided User-Generator PowerShell script, and save the file.

<img width="621" height="252" alt="image" src="https://github.com/user-attachments/assets/aac1e7ba-368f-4cbe-a142-ea9389f13e0e" />

Run the script and observe the additional user accounts being generated

<img width="622" height="308" alt="image" src="https://github.com/user-attachments/assets/2e74ab83-166b-4f60-b81e-0f3c3181d65c" />

Once the script finishes, open Active Directory Users and Computers and verify that the new accounts appear inside the _EMPLOYEES OU.


<img width="630" height="430" alt="image" src="https://github.com/user-attachments/assets/21c61330-7af6-46ea-b6f4-87e00da95b7e" />


Finally, use Remote Desktop Connection to access Client-1 with one of the newly created standard domain user accounts. Use the domain-qualified username format: mydomain.com\username

<img width="434" height="187" alt="image" src="https://github.com/user-attachments/assets/1e4ae886-6f90-4a57-a09d-03ddc33a8d92" />

Verify that the account successfully logs into Client-1.

<img width="620" height="343" alt="image" src="https://github.com/user-attachments/assets/67b70168-4e3c-4d17-b5c5-eb77732d5a9d" />


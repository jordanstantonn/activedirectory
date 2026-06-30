# Active Directory Home Lab (Windows 2022)
---
In this project, I built an Active Directory home lab using Windows Server 2022 and VirtualBox. The goal was to learn how to install Active Directory Domain Services (AD DS), promote a Windows Server to a domain controller, create a new Active Directory forest, and manage organizational units and user accounts.

[Video Demonstration Coming Soon](https://www.youtube.com/@jordanstantoncyber)
---
When the virtual machine starts, Server Manager opens automatically. Server Manager is a Windows Server tool used to install, configure, and manage server roles and features.
<img width="866" height="644" alt="image" src="https://github.com/user-attachments/assets/b3d7ec2c-6248-49d5-8df8-2af6f5d343a1" />


---

## 1. Renaming the Server

First, open the **Local Server** tab in Server Manager and rename the computer to make it easier to identify within the environment.

For this lab, the server was named:

- **ADLAB**
<img width="864" height="645" alt="image" src="https://github.com/user-attachments/assets/f039a558-62c2-453d-a2d2-696c50268673" />

After changing the computer name, Windows prompts for a restart to apply the change.

Once the server restarts, Server Manager opens automatically again, and the new computer name is displayed, confirming the change was successful.
<img width="858" height="647" alt="image" src="https://github.com/user-attachments/assets/3cd12bd3-1246-48fa-a9dd-02c0b82f9a18" />

---

## 2. Configuring a Static IP Address

Next, configure a static IP address for the server.

A domain controller (Active Directory server) needs a consistent IP address so it can always be found on the network. If DHCP were used and the IP changed, devices could lose connectivity and critical services like Active Directory and DNS could stop working.

### Network Settings:

Go to:

**Network Connections → Ethernet → Properties → Internet Protocol Version 4 (TCP/IPv4)**

Enter the following configuration:

- **IP Address:** 192.168.1.10  
- **Subnet Mask:** 255.255.255.0  
- **Default Gateway:** 192.168.1.1  
- **Preferred DNS:** 8.8.8.8  
- **Alternate DNS:** 8.8.4.4  
<img width="861" height="646" alt="image" src="https://github.com/user-attachments/assets/12ea045e-0312-49c4-92ac-b8f1ef27a30d" />

### Explanation:

- The IP address is set manually so the server remains reachable at a consistent address.
- The subnet mask defines the local network range.
- The default gateway allows communication outside the local network.
- DNS servers resolve domain names into IP addresses.

---

## 3. Installing Active Directory Domain Services (AD DS)

Next, install **Active Directory Domain Services (AD DS)**.

From the Server Manager dashboard:

1. Click **Add Roles and Features**
2. Click **Next** through the wizard until reaching **Server Roles**
3. Select **Active Directory Domain Services**
4. Click **Add Features** when prompted
5. Continue clicking **Next** through the wizard
6. On the **Confirmation** page, check:
   - Restart the destination server automatically if required
7. Click **Install**
<img width="865" height="645" alt="image" src="https://github.com/user-attachments/assets/7a7ba6b1-8409-4993-ba5d-8e9f8a11be73" />

This installs Active Directory, which is required to promote the server to a domain controller and manage users, computers, and network resources centrally.

---

## 4. Promoting the Server to a Domain Controller

After installation completes, return to the Server Manager dashboard.

Click the notification flag and select:

- **Promote this server to a domain controller**
<img width="859" height="652" alt="image" src="https://github.com/user-attachments/assets/92f0cb15-5505-415b-a82f-0b842b4a38d7" />

---

## 5. Creating a New Forest

Select:

- **Add a new forest**

Set the root domain name.

For this lab example:

- **stantonindustries.local**
<img width="859" height="644" alt="image" src="https://github.com/user-attachments/assets/56015533-f59c-476b-9393-bd6e2dbc2ddd" />

Click **Next** and create a Directory Services Restore Mode (DSRM) password when prompted.
<img width="861" height="643" alt="image" src="https://github.com/user-attachments/assets/6b1aea22-4f70-4271-8774-1e88373e1309" />

Continue clicking **Next** through the wizard.

On the **Prerequisites Check** page, verify that all requirements are met.

Click **Install** to proceed.
<img width="862" height="652" alt="image" src="https://github.com/user-attachments/assets/a171b5c1-3118-45f4-86fa-f0887c64b639" />

The system will automatically restart and sign out after installation completes.

---

## 6. Accessing Active Directory Users and Computers

After the restart:

1. Open **Server Manager**
2. Go to **Tools**
3. Select **Active Directory Users and Computers**

You should now see the domain listed and active.
<img width="858" height="647" alt="image" src="https://github.com/user-attachments/assets/327f97bb-d634-4172-b387-9589dae6bce7" />

---

## 7. Creating Organizational Units (OUs)

Next, create Organizational Units (OUs) to structure the directory.

Steps:

1. Right-click the domain
2. Select **New → Organizational Unit**
3. Name the OU based on your structure

For this project, the following OUs were created:

- **IT**
- **Finance**
- **HR**
<img width="162" height="342" alt="image" src="https://github.com/user-attachments/assets/01c72f4c-890a-455e-84eb-aedba30e6e32" />


---

## 8. Creating User Accounts

Inside each Organizational Unit (OU), user accounts can be created.

Steps:

1. Right-click the desired OU
2. Select **New → User**
3. Enter user details:
   - First name
   - Last name
   - Full name
   - User logon name
4. Create a password for the account
5. Configure account options as needed:
   - Require password change at next logon
   - User cannot change password
   - Password never expires
   - Disable account

---

## 9. Final Result

Users were successfully created inside their respective OUs:

- **IT Department**
  - Daniel
  - Caylee
  - Grobert
<img width="857" height="645" alt="image" src="https://github.com/user-attachments/assets/e58ba506-7d7f-431f-9cfc-0ed45b5a3133" />


- **Finance Department**
  - Harlin
  - Huy
  - Caelyn
  <img width="861" height="651" alt="image" src="https://github.com/user-attachments/assets/41b58c1c-6f5a-481b-b255-d448f3348e28" />


- **HR Department**
  - Jamelah
  - Johnny
  - Jordan
  <img width="864" height="649" alt="image" src="https://github.com/user-attachments/assets/0af03e78-2ee3-42a0-97d9-c1ad216e1ee9" />

---

This completes the installation of Active Directory Domain Services (AD DS), the promotion of the server to a domain controller, the creation of organizational units (OUs), the creation of users and groups, and the verification that Active Directory is working properly.

<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Deployment and Configuration Steps</h2>

Install Active Directory
Login to DC-1 and install Active Directory Domain Services

<img width="543" height="545" alt="image" src="https://github.com/user-attachments/assets/7e251b29-191e-4a6d-a665-a87b4a9da2cb" />


Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
Restart and then log back into DC-1 as user: mydomain.com\labuser

<img width="361" height="447" alt="image" src="https://github.com/user-attachments/assets/0731e9ad-d94b-4ce3-8b4e-0d107a7423c8" />

<img width="561" height="555" alt="image" src="https://github.com/user-attachments/assets/492905f0-bb8f-4211-8447-a9ca6120bc93" />


Create a Domain Admin user within the domain
—
In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
Create a new OU named “_ADMINS”

<img width="553" height="457" alt="image" src="https://github.com/user-attachments/assets/15d8b677-81f9-44e6-baad-7dbdbd858d9d" />


Create a new employee named “Jane Doe” (same password) with the username of “jane_admin” / Cyberlab123!

<img width="427" height="370" alt="image" src="https://github.com/user-attachments/assets/d569d63f-8ba4-4e6b-8c69-b993507620cd" />


Add jane_admin to the “Domain Admins” Security Group

<img width="404" height="525" alt="image" src="https://github.com/user-attachments/assets/b0b1e03b-b44b-447c-9357-389e0d6d0108" />


Log out / close the connection to DC-1 and log back in as “mydomain.com\jane_admin”
User jane_admin as your admin account from now on


Join Client-1 to your domain (mydomain.com)
—

Login to Client-1 as the original local admin (labuser) and join it to the domain (computer will restart)

<img width="313" height="386" alt="image" src="https://github.com/user-attachments/assets/74a06488-356b-40d9-b08a-8a87dd3fac29" />


Login to the Domain Controller and verify Client-1 shows up in ADUC
Create a new OU named “_CLIENTS” and drag Client-1 into there

Finish the lab, but do not delete the VMs in Azure. We will use them for upcoming labs.
If you are done for the day and want to save money, simply “Stop”/turn off the VMs within the Azure Portal

Part 2

Turn on the DC-1 and Client-1 VMs in the Azure Portal if they are off.
Setup Remote Desktop for non-administrative users on Client-1
—
Log into Client-1 as mydomain.com\jane_admin
Open system properties
Click “Remote Desktop”
Allow “domain users” access to remote desktop
You can now log into Client-1 as a normal, non-administrative user now
Normally you’d want to do this with Group Policy that allows you to change MANY systems at once (maybe a future lab)


Create a bunch of additional users and attempt to log into client-1 with one of the users
—
Login to DC-1 as jane_admin
Open PowerShell_ise as an administrator
Create a new File and paste the contents of the script into it
Run the script and observe the accounts being created
When finished, open ADUC and observe the accounts in the appropriate OU　(_EMPLOYEES)
attempt to log into Client-1 with one of the accounts (take note of the password in the script)

# AD-Setup-OU-User-Group-Policy-RMIT-Cybersecurity-Project
One of my Blue teaming labs from my [RMIT Cybersecurity Project](https://github.com/Kazu010101/RMIT-Cybersecurity-Project/blob/main/README.md)

## Objective

- Create 2 Organizational Units (OU): Admins and Consultants
- Create Users within the newly created OUs
- Create Groups
- Configure & Apply Password Policies into the Domain

## Lab Setup

- Windows Server 2022 VM Installed with Active Directory Domain Services (AD DS) role installed and configured as a domain controller.
- Windows 10 Pro VM Installed and Joined to the domain hosted on the Windows Server.
- Network Setting of both Windows Server and Windows 10 is 'internal'

## Create Organizational Units (OU)

- Step 1: Open the Active Directory Users and Computers (ADUC)
- Step 2: Right-click on xyzcompany.com in the left-hand pane > select New > Organizational Unit
- Step 3: Name the OU ("Admins") > Click OK
- *Repeat Step 2 & 3 to create the "Consultants" OU*

![aduc2](https://github.com/user-attachments/assets/b1333713-40db-4173-bb41-811e6cbaafdb)

## Result

A Windows Server VM with active Domain Controller and a Windows 10 VM which has been joined to the domain controller are created. The purpose is to simulate a real-world enterprise environment of centralized user authentication, group policy management, and security configurations which are essential for improving the security architecture of XYZ Company.

The next activity is to setup the AD such as creating Organizational Units (OU), user accounts and groups with different policies within the OUs. 

# AD-Setup-OU-User-Group-Policy-RMIT-Cybersecurity-Project
One of my Blue teaming labs from my [RMIT Cybersecurity Project](https://github.com/Kazu010101/RMIT-Cybersecurity-Project/blob/main/README.md)

## Objective

- Create 2 Organizational Units (OU): Admins and Consultants
- Create Users within the newly created OUs
- Create Groups
- Add Users into a Group
- Configure & Apply Password Policies into the Domain

## Lab Setup

- Windows Server 2022 VM Installed with Active Directory Domain Services (AD DS) role installed and configured as a domain controller.
- Windows 10 Pro VM Installed and Joined to the domain hosted on the Windows Server.
- Network Setting of both Windows Server and Windows 10 is 'internal'

## Create 2 Organizational Units (OU): Admins and Consultants

- Step 1: Open the Active Directory Users and Computers (ADUC).
- Step 2: Right-click on xyzcompany.com in the left-hand pane > select New > Organizational Unit.
- Step 3: Name the OU ("Admins") > Click OK.
- *Repeat Step 2 & 3 to create the "Consultants" OU.*

![aduc2](https://github.com/user-attachments/assets/b1333713-40db-4173-bb41-811e6cbaafdb)

We can verify the created OUs as they appear in the left pane of the ADUC console.

![aduc3](https://github.com/user-attachments/assets/7e0fbd8b-f61f-4a95-b27a-9f56b66cc474)

## Create Users within the newly created OUs

- Step 1: In the ADUC console, hover the cursor over the newly created OU (e.g., "Admins").
- Step 2: Right-click the selected OU and select New > User.
- Step 3: Fill out the user details (e.g., First Name, Last Name, and User Logon Name) > click Next.
- Step 4: Set up Password options as required, (e.g., User must change password at next logon) > click Finish.

![aduc4](https://github.com/user-attachments/assets/b88f6ce9-fb56-46cc-87a1-3757667bab24)

Repeat the steps to create multiple users as required.

![aduc5](https://github.com/user-attachments/assets/72c2a081-e343-4ad0-86a4-364c33820808)

## Create Groups

In the ADUC console, hover the cursor over the newly created OU (e.g., "Admins"):

- Step 1: Right-click the selected OU and select New > Group.
- Step 2: Fill out the group name and specify group scopes and types > click OK

![aduc6](https://github.com/user-attachments/assets/5f8da243-c9b4-4660-abba-ce2698f582af)
*The Group Scope of "Domain Local" and Group Type "Security" are selected to assign members' permissions to resources within the xyzcompany.com domain. This group can include members from any domain in the forest (users, groups, or computers).*

## Add Users into a Group

- Step 1: Double-click the group and go to the Members tab.
- Step 2: Click Add, type the user names, and click Check Names > click OK

![aduc7](https://github.com/user-attachments/assets/5ba0c1f6-41ed-4b75-8071-6b5c9be8e106)

Repeat the steps to add multiple users as required.

![aduc8](https://github.com/user-attachments/assets/0c864853-f992-40d0-b46b-1a7b73694f6e)

## Configure & Apply Password Policies into the Domain

- Step 1: Open the Group Policy Management console by click Tool > Group Policy Management
- Step 2: Expand the Forest: xyzcompany.com > double click "Domains" > double click xyz.company.com on the Domains pane
- Step 3: Click "Linked Group Policy Object" > right click "Default Domain Policy" > click Edit
- Step 4: Expand "Computer Configuration" > expand "Policies" > expand "Windows Settings" > expand "Security Settings" > expand "Account Policies" > right click "Password Policy" > click Open

![aduc9](https://github.com/user-attachments/assets/114b4091-5b3c-4f36-a184-1515975c05df)

- Step 5: From the revealed password settings available, right click on any of them and select Properties to configure the selected password policy > click Apply > click OK.

![aduc10](https://github.com/user-attachments/assets/e0a1512c-a561-4fcb-8367-f318cdb4f7d8)

- Step 6: Close the editor and run the command gpupdate /force in PowerShell as Administrator to apply the policy:

![aduc11](https://github.com/user-attachments/assets/93226806-cf25-49dd-adbf-6edd62dbb344)


## Result

The completion of this Active Directory lab simulates an improvement for xyz company in organizing users and groups within a domain, ensuring clear role-based access control, and centralizing management. Furthermore, implementing password policies and structuring users into OUs and groups are necessary control to minimizing unauthorized access and improving overall domain security posture.

The next activity is to setup pfSense VM so that the Windows Server VM and all computers joined with the domain can have internet access.

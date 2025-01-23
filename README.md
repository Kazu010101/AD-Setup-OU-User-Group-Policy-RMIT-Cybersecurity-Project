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
- Step 3: Fill out the user details (e.g., First Name "Admin", Last Name "One", and User Logon Name "Admin1") > click Next.
- Step 4: Set up Password options as required, (e.g., User must change password at next logon) > click Finish.

![aduc4](https://github.com/user-attachments/assets/b88f6ce9-fb56-46cc-87a1-3757667bab24)

Repeat the steps to create "Admin Two" on the Admins OU, and "Consultant One" and "Consultant Two" on the Consultants OU.

![aduc5](https://github.com/user-attachments/assets/72c2a081-e343-4ad0-86a4-364c33820808)

## Create Groups

In the ADUC console, hover the cursor over the newly created OU (e.g., "Admins"):

- Step 1: Right-click the selected OU and select New > Group.
- Step 2: Fill out the group name "Classified Infomation" and specify group scopes and types > click OK

![aduc6](https://github.com/user-attachments/assets/5f8da243-c9b4-4660-abba-ce2698f582af)

*The Group Scope of "Domain Local" and Group Type "Security" are selected to assign members' permissions to resources within the xyzcompany.com domain. This group can include members from any domain in the forest (users, groups, or computers).*

## Add Users into a Group

- Step 1: Double-click the group and go to the Members tab.
- Step 2: Click Add, type the user name "Admins One", and click Check Names > click OK

![aduc7](https://github.com/user-attachments/assets/5ba0c1f6-41ed-4b75-8071-6b5c9be8e106)

Repeat the steps to add the user 'Admin Two' into "Classified Information" Group.

![aduc8](https://github.com/user-attachments/assets/0c864853-f992-40d0-b46b-1a7b73694f6e)

## Configure & Apply Password Policies into the Domain

- Step 1: Open the Group Policy Management console by click Tool > Group Policy Management
- Step 2: Expand the Forest: xyzcompany.com > double click "Domains" > double click xyz.company.com on the Domains pane
- Step 3: Click "Linked Group Policy Object" > right click "Default Domain Policy" > click Edit
- Step 4: Expand "Computer Configuration" > expand "Policies" > expand "Windows Settings" > expand "Security Settings" > expand "Account Policies" > right click "Password Policy" > click Open

![aduc9](https://github.com/user-attachments/assets/114b4091-5b3c-4f36-a184-1515975c05df)

- Step 5: From the revealed password settings available, right click on any of them and select Properties to configure the selected password policy > click Apply > click OK.

![aduc10](https://github.com/user-attachments/assets/e0a1512c-a561-4fcb-8367-f318cdb4f7d8)

- Step 6: Close the editor and run the command `gpupdate /force` in PowerShell as Administrator to apply the policy:

![aduc11](https://github.com/user-attachments/assets/93226806-cf25-49dd-adbf-6edd62dbb344)

## Verification of Group Policy

At this point, the "Classified Information" Group created before comprises of 2 users only, which are "Admin One" and "Admin Two". We can verify that other users who are not joined in the group cannot access the folder by creating a Shared Folder on the Windows Server VM and configuring the permission as follows:

- Create a folder on the C: drive (C:\Classified Information).
- Right-click the folder, select Properties, and go to the Sharing tab.
- Click Advanced Sharing, check Share this folder, and click Permissions.
- Remove the default Everyone group and click Add.
- Type the group name "Classified Information" and click Check Names.
- Grant Full Control permissions and click OK.
- Confirm sharing settings and close the dialog.

Next, we setup the NTFS permissions:
- Go to the Security tab in the folder’s properties.
- Click Edit, then Add, and enter the group name "Classified Information".
- Set NTFS permissions ("Full Control") and click OK.

Log-in as Consultant Two (Non-Group Member) on the Windows 10 VM:
- Open File Explorer and type the shared folder’s UNC path `\\SVR01` in the address bar

![aduc12](https://github.com/user-attachments/assets/76114d81-2dad-483b-b4f2-e4659534fa7a)

- Double Click on the "Classified Information" Folder and the prompt will show Access Denied.

![aduc13](https://github.com/user-attachments/assets/d9c257bf-b2af-4d5c-8020-b77da4a56637)

Log out from the user 'Consultant Two' and re-login into Windows 10 VM as 'Admin Two' to verify that an authorized member could access the "Classified Information" Shared Folder:

![aduc14](https://github.com/user-attachments/assets/03754e11-b39a-4aad-9f72-62f6cdf84410)


## Result

The completion of this Active Directory lab simulates an improvement for xyz company in organizing users and groups within a domain, ensuring clear role-based access control, and centralizing management. Furthermore, implementing password policies and structuring users into OUs and groups are necessary control to minimizing unauthorized access and improving overall domain security posture.

The next activity is to install pfSense VM and link it with the Windows Server VM so that the server and computers joined in the domain have access to the internet.


<h1>Managing Network File Shares & Permissions</h1>

This lab focuses on creating and managing network file shares and permissions in a Windows domain environment. We'll use Azure virtual machines to configure shared folders, apply access permissions, and test security settings. The lab emphasizes understanding how user roles and group memberships affect file access.<br />
<br />
<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- PowerShell
<br />
<br />

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
<br />
<br />

<h2>Walkthrough Steps</h2>

1. Setup
  - Power on the DC-1 (domain controller) and Client-1 virtual machines in Azure
  - Log into DC-1 as mydomain.com\jane_admin<br />
      ![image](https://github.com/user-attachments/assets/dc0d88f9-3a96-44b3-919a-cccc30cd7c35)
  - Log into Client-1 as a normal user (e.g., mydomain\someuser)<br />
      ![image](https://github.com/user-attachments/assets/e1b93516-000e-48e0-8c73-fbf28cdb4365)
<br />
<br />

2. Create Shared Folders and Apply Permissions
  - On DC-1, create the following folders on the C:\ drive:
  - read-access, write-access, no-access, accounting<br />
      ![image](https://github.com/user-attachments/assets/2ef618b0-18e3-4a82-8f06-3b02c86a34c2)
  - Apply permissions for each folder:
    - read-access: Assign the Domain Users group with Read permissions<br />
        ![image](https://github.com/user-attachments/assets/708a29a3-ecf5-4610-af3c-af60a21f47c8)
    - write-access: Assign the Domain Users group with Read/Write permissions<br />
        ![image](https://github.com/user-attachments/assets/867a908f-78bf-4911-b53c-118dff639026)
    - no-access: Assign the Domain Admins group with Read/Write permissions<br />
        ![image](https://github.com/user-attachments/assets/e8c54228-ea97-4a8f-8157-15446dc7ef85)
  - Share the folders using their respective names
<br />
<br />

3. Test Folder Access
  - On Client-1, navigate to the shared folders using \\dc-1 in the Run dialog<br />
      ![image](https://github.com/user-attachments/assets/3a48a36d-318a-4de3-a3a6-788bb30d7dee)
  - Test access to each folder:
    - Verify which folders are accessible<br />
        ![image](https://github.com/user-attachments/assets/b5460437-c296-448f-a736-06d4f39d43a8)
        ![image](https://github.com/user-attachments/assets/1496f559-f00e-4fa9-b9b6-d64fe23d3f76)
        ![image](https://github.com/user-attachments/assets/4d709afa-8d91-4e6f-88d7-5187ce1b24af)
    - Confirm whether you can create files in the folders with write permissions<br />
        ![image](https://github.com/user-attachments/assets/50c08c1e-984c-41ad-85a5-f78eaed32f35)
<br />
<br />

4. Create Security Group and Test Permissions
  - On DC-1, create a new security group in Active Directory called ACCOUNTANTS<br />
      ![image](https://github.com/user-attachments/assets/dbb551a3-4b6f-43fc-a87b-3ff00b3df0d3)
  - Assign permissions to the accounting folder:
    - Grant the ACCOUNTANTS group Read/Write permissions<br />
        ![image](https://github.com/user-attachments/assets/e445bc34-0a42-4ea4-a474-0e1f4028fe2c)
  - Test access:
    - On Client-1, as the normal user (someuser), attempt to access the accounting folder. It should fail<br />
        ![image](https://github.com/user-attachments/assets/d79e33ae-5977-4d8f-9f1a-2a7992c7e90a)
  - Update group membership:
    - On DC-1, add the user (someuser) to the ACCOUNTANTS security group<br />
        ![image](https://github.com/user-attachments/assets/3a4f2d21-8a1e-472a-84ea-61091f57927f)
  - Test access again:
    - Log out and back into Client-1 as someuser
    - Attempt to access the accounting folder. It should now succeed<br />
        ![image](https://github.com/user-attachments/assets/287d8097-6f9b-4128-b234-fb27fc89e806)
<br />
<br />

5. Cleanup
  - If you are done with the lab, you may delete the VMs. Alternatively, keep them for further practice
<br />
<br />

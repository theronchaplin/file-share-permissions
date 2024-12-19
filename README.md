
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
  - Log into DC-1 as mydomain.com\jane_admin and Client-1 as a normal user (e.g., mydomain\someuser)
<br />
<br />

2. Create Shared Folders and Apply Permissions
  - On DC-1, create the following folders on the C:\ drive:
  - read-access, write-access, no-access, accounting
  - Apply permissions for each folder:
    - read-access: Assign the Domain Users group with Read permissions
    - write-access: Assign the Domain Users group with Read/Write permissions
    - no-access: Assign the Domain Admins group with Read/Write permissions
  - Share the folders using their respective names
<br />
<br />

3. Test Folder Access
  - On Client-1, navigate to the shared folders using \\dc-1 in the Run dialog
  - Test access to each folder:
    - Verify which folders are accessible
    - Confirm whether you can create files in the folders with write permissions
<br />
<br />

4. Create Security Group and Test Permissions
  - On DC-1, create a new security group in Active Directory called ACCOUNTANTS
  - Assign permissions to the accounting folder:
    - Grant the ACCOUNTANTS group Read/Write permissions
  - Test access:
    - On Client-1, as the normal user (someuser), attempt to access the accounting folder. It should fail
  - Update group membership:
    - On DC-1, add the user (someuser) to the ACCOUNTANTS security group
  - Test access again:
    - Log out and back into Client-1 as someuser
    - Attempt to access the accounting folder. It should now succeed
<br />
<br />

5. Cleanup
  - If you are done with the lab, you may delete the VMs. Alternatively, keep them for further practice
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/kcq30PT.png" alt="Traffic Examination"/>
</p>

<h1>Network File Shares and Permissions-Sharing and Accessing Folders over a Network Azure Virtual Machines</h1>
In this tutorial,These steps provide a comprehensive guide to setting up and verifying folder permissions in a Windows domain environment.





<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools


<h2>Operating Systems Used </h2>

- Windows 10 (21H2)

<h2>High-Level Steps</h2>

<h2>Actions and Observations</h2>

<p>
<img src="https://imgur.com/o3GMvPW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
1. Log into Domain Controller (DC1):
First, I open the Azure portal and navigate to Virtual Machines.
I connect to my Domain Controller VM (DC1) using Remote Desktop.
I log in with the administrator credentials (e.g., Jane_admin).
</p>
<br />

<p>
<img src="https://imgur.com/lDzr897.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
2. Create Folders:
On DC1, I open File Explorer and navigate to the C: drive.
I create four folders named: ReadAccess, WriteAccess, NoAccess, and Accounting.
</p>
<br />

<p>
<img src="https://imgur.com/ttPdXwx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
3. Share the Folders:

I right-click on ReadAccess, go to Properties, then the Sharing tab, and click Advanced Sharing.
I check Share this folder, and set the share name to ReadAccess.
I click on Permissions, add Domain Users, and set their permission to Read. Then I click OK.
I repeat the above steps for the WriteAccess folder, but set the permissions to Full Control for Domain Users.
For NoAccess, I only add Domain Admins with Full Control.
For Accounting, I add specific users or groups with the desired access levels as per my organization's requirements.
</p>
<br />

<p>
<img src="https://imgur.com/8ggBknu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
4. I open File Explorer on Client1.
In the address bar, I type \\DC1\ReadAccess and press Enter. I should have read-only access to this folder.
I try accessing \\DC1\WriteAccess and verify that I can create and delete files.
I access \\DC1\NoAccess to confirm that I do not have permission to view this folder (unless I am logged in as an admin).
I access \\DC1\Accounting and test the permissions as configured.
</p>
<br />

<p>
<img src="https://imgur.com/1duxuLF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
5. On DC1, I open the Active Directory Users and Computers tool.
I navigate to my domain, right-click on Users, and select New > Group.
I name the group AccountingUsers and set the group scope to Global and group type to Security. Then I click OK.
I repeat the process to create additional groups such as ReadOnlyUsers, WriteUsers, etc.


</p>
<br />

<p>
<img src="https://imgur.com/T2n1u4F.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
6. Security Group Creation:

Created a new security group named "Accountants" in Active Directory Users and Computers.
Assigned "Accountants" read and write permissions to the "Accounting" folder.
</p>
<br />

<p>
<img src="https://imgur.com/zBA28u9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
7. I go back to the folder properties for each shared folder on DC1.
For Accounting, I go to the Security tab, click Edit, and then Add.
I enter the name of the group AccountingUsers and set the appropriate permissions (e.g., Read and Write).
I click OK.

I repeat the process for other folders and assign the groups I created with the respective permissions.
</p>
<br />

<p>
<img src="https://imgur.com/nZlFgTG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
8. Testing Access from Client1:
Logged into Client1 as a generic user to confirm that access to the "Accounting" folder was initially denied.
Added the user to the "Accountants" security group and attempted to access the folder again.
</p>
<br />

<p>
<img src="https://imgur.com/HtAYOpo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
9. Add User to Group:
Added the generic user (bodap) to the "Accountants" group in Active Directory Users and Computers.
</p>
<br />






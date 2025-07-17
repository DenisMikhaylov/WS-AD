Managing user settings with Group Policy

Scenario

A. Datum Corporation has implemented Microsoft Office 2016, and you want to use Group Policy to
configure settings for some Office 2016 apps. The IT department uses logon scripts to provide users with
drive mapping to shared folders. However, maintaining these scripts is an ongoing problem, because they
are large and complex. Your manager has asked that you implement drive mapping by using Group Policy
preferences to remove logon scripts.
Your manager also has asked that you place a desktop shortcut to the Notepad app for all users who
belong to the IT Security group. Additionally, you must add a new computer administrator’s security group
as a local administrator on all servers.
To help minimize profile sizes, you also need to configure Folder Redirection to redirect several profile
folders to each user’s home drive. Finally, you have to complete the GPO design to manage user desktops
and server security.
Objectives

After completing this lab, you will be able to:
Use administrative templates to manage user settings.
Implement settings by using Group Policy preferences.
Configure Folder Redirection.


Managing user settings with Group
Policy

Exercise 0: Creating and managing object in AD DS
```
New-ADOrganizationalUnit -Name:"Managers" -Path:"DC=ADATUM,DC=COM" -ProtectedFromAccidentalDeletion:$true -Server:"LON-DC1.ADATUM.COM"
New-ADOrganizationalUnit -Name:"Research" -Path:"DC=ADATUM,DC=COM" -ProtectedFromAccidentalDeletion:$true -Server:"LON-DC1.ADATUM.COM"
New-ADOrganizationalUnit -Name:"Marketing" -Path:"DC=ADATUM,DC=COM" -ProtectedFromAccidentalDeletion:$true -Server:"LON-DC1.ADATUM.COM"
New-ADOrganizationalUnit -Name:"Development" -Path:"DC=ADATUM,DC=COM" -ProtectedFromAccidentalDeletion:$true -Server:"LON-DC1.ADATUM.COM"
New-ADOrganizationalUnit -Name:"IT" -Path:"DC=ADATUM,DC=COM" -ProtectedFromAccidentalDeletion:$true -Server:"LON-DC1.ADATUM.COM"

New-ADGroup -GroupCategory:"Security" -GroupScope:"Global" -Name:"Managers" -Path:"OU=Managers,DC=ADATUM,DC=COM" -SamAccountName:"Managers" -Server:"LON-DC1.ADATUM.COM"
New-ADGroup -GroupCategory:"Security" -GroupScope:"Global" -Name:"Research" -Path:"OU=Research,DC=ADATUM,DC=COM" -SamAccountName:"Research" -Server:"LON-DC1.ADATUM.COM"
New-ADGroup -GroupCategory:"Security" -GroupScope:"Global" -Name:"Marketing" -Path:"OU=Marketing,DC=ADATUM,DC=COM" -SamAccountName:"Marketing" -Server:"LON-DC1.ADATUM.COM"
New-ADGroup -GroupCategory:"Security" -GroupScope:"Global" -Name:"Development" -Path:"OU=Development,DC=ADATUM,DC=COM" -SamAccountName:"Development" -Server:"LON-DC1.ADATUM.COM"
New-ADGroup -GroupCategory:"Security" -GroupScope:"Global" -Name:"IT" -Path:"OU=IT,DC=ADATUM,DC=COM" -SamAccountName:"IT" -Server:"LON-DC1.ADATUM.COM"

$password='Pa55w.rd' | ConvertTo-SecureString -AsPlainText -Force

New-ADUser -City:"London" -Company:"Adatum" -Department:"IT" -DisplayName:"Abbi Skinner" -GivenName:"Abbi" -Surname:"Skinner" -Name:"Abbi Skinner" -UserPrincipalName:"Abbi@ADATUM.COM" -SamAccountName:"Abbi" -Path:"OU=IT,DC=ADATUM,DC=COM"  -Server:"LON-DC1.ADATUM.COM"  -Type:"user" -AccountPassword $password -Enabled $true
New-ADUser -City:"London" -Company:"Adatum" -Department:"IT" -DisplayName:"Beth Burke" -GivenName:"Beth" -Surname:"Burke" -Name:"Beth Burke" -Path:"OU=IT,DC=ADATUM,DC=COM" -SamAccountName:"Beth" -Server:"LON-DC1.ADATUM.COM" -Type:"user" -UserPrincipalName:"Beth@ADATUM.COM" -AccountPassword $password -Enabled $true
New-ADUser -City:"London" -Company:"Adatum" -Department:"IT" -DisplayName:"Dante Dabney" -GivenName:"Dante" -Surname:"Dabney"  -Name:"Dante Dabney" -Path:"OU=IT,DC=ADATUM,DC=COM" -SamAccountName:"Dante" -Server:"LON-DC1.ADATUM.COM" -Type:"user" -UserPrincipalName:"Dante@ADATUM.COM" -AccountPassword $password -Enabled $true
New-ADUser -City:"London" -Company:"Adatum" -Department:"Research" -DisplayName:"Cai Chu" -GivenName:"Cai" -Surname:"Chu" -Name:"Cai Chu" -UserPrincipalName:"Cai@ADATUM.COM" -SamAccountName:"Cai" -Path:"OU=Research,DC=ADATUM,DC=COM"  -Server:"LON-DC1.ADATUM.COM"  -Type:"user" -AccountPassword $password -Enabled $true
New-ADUser -City:"London" -Company:"Adatum" -Department:"Research" -DisplayName:"Connie Vaughn" -GivenName:"Connie" -Surname:"Vaughn" -Name:"Connie Vaughn" -UserPrincipalName:"Connie@ADATUM.COM" -SamAccountName:"Connie" -Path:"OU=Research,DC=ADATUM,DC=COM"  -Server:"LON-DC1.ADATUM.COM"  -Type:"user" -AccountPassword $password -Enabled $true
```

Exercise 1: Using administrative templates to manage user settings

Task 1: Import administrative templates for Microsoft Office 2016
1. On LON-DC1, on the taskbar, click the File Explorer icon.
2. In File Explorer, in the navigation pane, expand Allfiles (E:), expand Labfiles, and then click Mod06.
3. Double-click admintemplates_x64_4390-1000_en-us.exe.
4. In The Microsoft Office 2016 Administrative Templates dialog box, select the Click here to accept
the Microsoft Software License Terms check box, and then click Continue.
5. In the Browse for Folder dialog box, click Desktop, and then click OK.
6. In The Microsoft Office 2016 Administrative Templates dialog box, click OK.
7. In File Explorer, in the navigation pane, click Desktop, and then in the content pane, double-click
admx.
8. Press Ctrl+A to select all files, right-click, and then click Copy.
9. In the navigation pane, expand Local Disk (C:), expand Windows, right-click PolicyDefinitions, and
then click Paste.
10. Close File Explorer.

Task 2: Configure Office 2016 settings
1. On LON-DC1, in Server Manager, click Tools, and then click Group Policy Management.
2. Switch to the Group Policy Management window.
3. In the navigation pane, expand Forest: Adatum.com, expand Domains, expand Adatum.com, and
then click Group Policy Objects.
4. Right-click Group Policy Objects, and then click New.
5. In the New GPO dialog box, type Office 2016 settings, and then click OK.
6. In the contents pane, right-click Office 2016 settings, and then click Edit.
7. In the Group Policy Management Editor, in the navigation pane, expand User Configuration,
expand Policies, expand Administrative Templates, and then click Microsoft Excel 2016.
8. Expand Microsoft Excel 2016, expand Excel Options, click Customize Ribbon, and then double-click
Display Developer tab in the Ribbon.
9. In the Display Developer tab in the Ribbon dialog box, click Enabled, and then click OK.
10. In the Group Policy Management Editor, click Save, and then double-click Default file location.
11. In the Default file location dialog box, click Enabled, in the Default file location text box, type
%userprofile%\Desktop, and then click OK.
12. Close the Group Policy Management Editor.
13. In Group Policy Management, right-click the Adatum.com domain, and then click Link an
Existing GPO.
14. In the Select GPO dialog box, click Office 2016 settings, and then click OK.

Exercise 2: Implementing settings by using Group Policy preferences

Scenario

You now have to implement drive mapping by using Group Policy preferences to remove logon scripts that
A. Datum uses currently to provide users with drive mapping to shared folders. You also need to place a
desktop shortcut to the Notepad app for all users who belong to the IT Security group.
The main tasks for this exercise are as follows:
1. Set up the current environment.
2. Test mapped drive for Branch Office 1 users.
3. Create a Preferences GPO with the required Group Policy preferences.
4. Test the preferences

Task 1: Set up the current environment
1. Switch to LON-DC1.
2. On LON-DC1, on the taskbar, click the File Explorer icon.
3. In the navigation pane, expand Allfiles (E:), expand Labfiles, and then click Mod06.
4. In the details pane, right-click Mod06-1.ps1, and then click Run with PowerShell.
5. If prompted, type Y, and then press Enter.
6. Right-click BranchScript.cmd, and then click Copy.
7. Switch to the Group Policy Management window.
8. In the navigation pane, right-click Group Policy Objects, and then click Refresh.
9. Right-click the Branch1 Group Policy Object (GPO), and then click Edit.
10. In the Group Policy Management Editor window, under User Configuration, expand Policies,
expand Windows Settings, and then click Scripts (Logon/Logoff).
11. In the details pane, double-click Logon.
12. In the Logon Properties dialog box, click Show Files.
13. In the details pane, right-click a blank area, and then click Paste.
14. Close the Logon window.
15. In the Logon Properties dialog box, click Add.
16. In the Add a Script dialog box, click Browse.
17. Click BranchScript.cmd, and then click Open.
18. Click OK twice to close all dialog boxes.
19. Close the Group Policy Management Editor window.

Task 2: Test mapped drive for Branch Office 1 users
1. Switch to LON-SVR1
2. Right-click Start, hover over Shut down or sign out, and then click Restart.
3. When the computer has restarted, sign in as Adatum\Abbi with the password Pa55w.rd.
4. On the taskbar, click the File Explorer icon.
5. In File Explorer, click This PC.
6. Verify that in the details pane, in the Network Locations section, drive S displays.
7. If drive S is not available, perform these steps:
a. Right-click Start, and click Command Prompt.
b. In the Command Prompt window, type the following two commands, and press Enter after each
command:
Gpupdate /force
Shutdown /r /t 0
c. Perform steps 3-6 again.


Task 3: Create a Preferences GPO with the required Group Policy preferences
1. Switch to LON-DC1.
2. On LON-DC1, switch to Server Manager, click Tools and then click Active Directory Users and
Computers.
3. In the Active Directory Users and Computers window, right-click IT, hover over New, and then click
Group.
4. In the New Object – Group dialog box, in the Group name text box, type Computer Administrators,
and then click OK.
5. Switch to the Group Policy Management Console, right-click the Adatum.com domain, and then
click Refresh.
6. Expand Branch Office 1, right-click the Branch1 GPO, and then click Delete.
7. In the Group Policy Management dialog box, click OK.
8. Right-click the Adatum.com domain, and then click Create a GPO in this domain, and Link it here.
9. In the New GPO dialog box, in the Name text box, type Preferences, and then click OK.
10. In the navigation pane, right-click Preferences, and then click Edit.
11. Expand User Configuration, expand Preferences, expand Windows Settings, right-click Shortcuts,
hover over New, and then click Shortcut.
12. In the New Shortcut Properties dialog box, in the Action list, click Create.
13. In the Name text box, type Notepad.
14. In the Location box, click the arrow, and then select All Users Desktop.
15. In the Target path box, type C:\Windows\System32\Notepad.exe.
16. On the Common tab, clear the Run in logged-on user’s security context (user policy option) check
box.
17. Select the Item-level targeting check box, and then click Targeting.
18. In the Targeting Editor dialog box, click New Item, and then click Security Group.
19. In the lower part of the dialog box, click the ellipsis button (…).
20. In the Select Group dialog box, in the Enter the object name to select (examples) box, type IT, and
then click OK.
21. Click OK two more times.
22. Right-click Drive Maps, hover over New, and then click Mapped Drive.
23. In the New Drive Properties dialog box, in the Location text box, type \\LON-DC1\Branch1, and
then select the Reconnect check box. In the Label as text box, type Drive for Branch Office 1, in the
Use drop-down list box, select S.
24. On the Common tab, select the Run in logged-on user’s security context (user policy option)
check box.
25. Select the Item-level targeting check box, and then click Targeting.
26. In the Targeting Editor dialog box, click New Item, and then click Organizational Unit.
27. In the lower part of the dialog box, click the ellipsis button (…).
28. In the Find Custom Search dialog box, in the Search results list, select Branch Office 1, and then
click OK.
29. Click OK two more times.
30. Expand Computer Configuration, expand Preferences, and then expand Control Panel Settings.
31. Right-click Local Users and Groups, hover over New, and then click Local Group.
32. In the New Local Group Properties dialog box, in the Group name text box, type Administrators,
and then click Add.
33. In the Local Group Member dialog box, click the ellipsis button (…).
34. In the Select User, Computer or Group dialog box, in the Enter the object name to select
(examples) text box, type Computer Administrators, and then click OK twice.
35. In the New Local Group Properties dialog box, click the Common tab.
36. On the Common tab, select the Item-level targeting check box, and then click Targeting.
37. In the Targeting Editor dialog box, click New Item, and then click Operating System.
38. In the Product drop-down list box, select Windows Server 2016 Family, and then click OK twice.
39. Close all open windows except Group Policy Management and Server Manager.

Task 4: Test the preferences
1. Switch to LON-SVR1
2. Right-click Start, hover over Shut down or sign out, and then click Restart.
3. When the computer has restarted, sign in as Adatum\Abbi with the password Pa55w.rd.
4. On the taskbar, click the File Explorer icon.
5. In File Explorer, click This PC.
6. Verify that in the details pane, in the Network Locations section, drive S displays.
Note: The drive label now is Drive for Branch Office 1, which verifies that the drive is
mapped through Group Policy preferences.
7. On the desktop, verify that a shortcut exists for Notepad.
8. If the shortcut for Notepad is not available, perform these steps:
a. Right-click Start, and click Command Prompt.
b. In the Command Prompt window, type the following two commands, and press Enter after each
command:
Gpupdate /force
Shutdown /r /t 0
c. Perform step 3 again.
The shortcut for Notepad should now display on the desktop.
9. Right-click Start, and then click Computer Management.
10. In Computer Management, expand Local Users and Groups, and then click Groups.
11. In the details pane, double-click Administrators.
12. Verify that the Computer Administrators group is not a member of the Administrators group.
Note: The Computer Administrators group is not a member of the Administrators group
because the Preferences setting only applies to servers.
13. Sign out of LON-SVR1

Exercise 3: Configuring Folder Redirection

Scenario

To help minimize profile sizes, you decide to configure Folder Redirection for the branch office users, to
redirect several profile folders to each user’s home drive.
The main tasks for this exercise are as follows:
1. Create a shared folder to store the redirected folders.
2. Create a new GPO and link it to the Branch Office 1 organizational unit (OU).
3. Edit the Folder Redirection settings in the policy.
4. Test the Folder Redirection settings

Task 1: Create a shared folder to store the redirected folders
1. On LON-DC1, on the taskbar, click the File Explorer icon.
2. In the navigation pane, click This PC.
3. In the details pane, double-click Local Disk (C:), and then on the Home tab, click New folder.
4. Name the new folder Branch1Redirect.
5. Right-click the Branch1Redirect folder, click Share with, and then click Specific people.
6. In the File Sharing dialog box, click the drop-down list box, select Everyone, and then click Add.
7. For the Everyone group, click the Permission Level drop-down list box, and then click Read/Write.
8. Click Share, and then click Done.
9. Close File Explorer.

Task 2: Create a new GPO and link it to the Branch Office 1 organizational unit (OU)
1. On LON-DC1, switch to Group Policy Management.
2. In Group Policy Management, expand and right-click Branch Office 1, and then click Create a GPO in
this domain and Link it here.
3. In the New GPO dialog box, in the Name text box, type Folder Redirection, and then click OK.

Task 3: Edit the Folder Redirection settings in the policy
1. Expand Branch Office 1, right-click Folder Redirection, and then click Edit.
2. In the Group Policy Management Editor window, under User Configuration, expand Policies,
expand Windows Settings, and then expand Folder Redirection.
3. Right-click Documents, and then click Properties.
4. In the Document Properties dialog box, on the Target tab, in the Setting drop-down list box, select
Basic – Redirect everyone’s folder to the same location.
5. Ensure that the Target folder location box is set to Create a folder for each user under the
root path.
6. In the Root Path text box, type \\LON-DC1\Branch1Redirect, and then click OK.
7. In the Warning dialog box, click Yes.
8. Right-click Pictures, and then click Properties.
9. In the Pictures Properties dialog box, on the Target tab, in the Setting drop-down list box, select
Follow the Documents folder, and then click OK.
10. In the Warning dialog box, click Yes.
11. Right-click Music, and then click Properties.
12. In the Music Properties dialog box, on the Target tab, in the Setting drop-down list box, select
Follow the Documents folder, and then click OK.
13. In the Warning dialog box, click Yes.
14. Close all open windows on LON-DC1.

Task 4: Test the Folder Redirection settings
1. Switch to LON-SVR1
2. Sign in as Adatum\Abbi with the password Pa55w.rd.
3. Right-click Start, and then click Command Prompt.
4. In the Command Prompt window, type the following command, and then press Enter:
gpupdate /force
5. When prompted, type the following and then press Enter:
Y
6. Sign out, and then sign back in to LON- as Adatum\Abbi with the password Pa55w.rd.
7. On the taskbar, click the File Explorer icon.
8. In File Explorer, in the navigation pane, right-click Documents, and then click Properties.
9. In the Documents properties dialog box, verify that the location is
\\LON-DC1\Branch1Redirect\Abbi, and then click OK.
Note: If the location is C:\Users\Abbi, perform steps 3 through 9 again. If the location has
not changed, restart LON- and perform steps 2 through 9 again.
10. Click Documents, and verify that two subfolders, Music and Pictures exist.
Note: This verifies that Music and Pictures are redirected as well.
11. Sign out of LON-

Exercise 4: Planning Group Policy (optional)

Scenario

You are tasked with planning a GPO model for the current infrastructure to manage security for the user
desktops and servers. You need to finalize the delegation model for administrative tasks, and determine the
administrators who will have rights on the client computers.
A. Datum management also wants you to configure Windows Update settings, and restrict administrative
tools for regular user accounts. Additionally, one of the security requirements is that the company have a
compliance warning related to misuse of corporate computers.
As the administrator of A. Datum, you are tasked with translating the business requirements into GPO
settings. You must then design and implement the GPOs at the appropriate levels of the OU design

In this exercise, you will design the GPO strategy that meets the business and organizational requirements
for A. Datum.

Supporting Documentation

Beth Burke

From: Huong Tang [Huong@adatum.com]
Sent: 2nd July 11:43
To: Beth@adatum.com
Subject: GPO Design
Hello Beth,
As we’ve discussed in our meeting yesterday, we need to strengthen the security of servers and configure
the users’ desktops according to the first initial design.
I’ve included the notes of our meeting in the attached proposal document. Please read the document.
Also, it would be great if you could send me the updated proposal document later this week.
Thank you very much,
Huong

A. Datum GPO Strategy Proposal

Document Reference Number: BS00918/1

Document Author Beth Burke

Date  2nd July


Requirements Overview

Design a GPO strategy that meets the following requirements:

All the organization’s computers should have a core group of GPO settings that must be applied. These
settings should include:
o Configuring the local administrator accounts.
o Configuring update settings.
o Restricting certain options, such as access to the registry editor.
These settings should not apply to administrator desktops.
 
Each office should have a core group of settings that apply to their workstations. As of now, you need
to implement the following:
o Display a security warning prior to computer sign-in stating that only A. Datum employees can use
the computers. This setting needs to be applied to each location, and to display automatically in
other languages for foreign locations.
 All users must have a default set of mapped drives assigned to them. You should base the mapped
drive on the department membership.
 The central IT administrators in London must be able to manage all GPOs and settings in the
organization. Administrators in each office should be able to manage only GPOs that apply to that
office.

A. Datum GPO Strategy Proposal

Summary of Information
The supporting OU structure includes the following:
Users are currently grouped by department in a top-level OU.
Clients are in the top-level Clients OU, which is separated by location on the next level.

Proposals
Which of the requirements will necessitate creating one or more GPOs?
Can you fulfill any of the requirements without creating GPOs?
Are there any exceptions to the default GPO application that you must consider?
List the GPOs that you must create to fulfill the lab scenario’s requirements. Provide the following
information in the table provided:
o Name of the GPO
o The requirements that the GPO fulfills
o The configuration settings (user policies, computer policies, user preferences, or computer
preferences) that the GPO will contain
o The container (domain, OU, site) to which the GPO will be linked

The main tasks for this exercise are as follows:
1. Read the supporting documentation.
2. Update the proposal document with your planned course of action.
5. Prepare for the next module.


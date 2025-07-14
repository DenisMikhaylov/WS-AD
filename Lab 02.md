
Managing AD DS objects

Scenario
You have been working for A. Datum Corporation as a desktop support specialist and have visited desktop
computers to troubleshoot app and network problems. You recently accepted a promotion to the server
support team. One of your first assignments is to configure the infrastructure service for a new branch
office.

To begin deployment of the new branch office, you are preparing AD DS objects. As part of this
preparation, you need to create users and groups for the new branch office that will house the Research
department. Finally, you need to reset the secure channel for a computer account that has lost connectivity
to the domain in the branch office.

Objectives
After completing this lab, you will have:
Created and configured groups in AD DS.
Created and configured user accounts in AD DS.
Managed computer objects in AD DS.
Lab Setup
Estimated Time: 45 minutes
Virtual machines: LON-DC1 and LON-SVR2
User name: Adatum\Administrator
Password: Pa55w.rd

Exercise 1: Creating and managing object in AD DS
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

```

Exercise 1: Creating and managing groups in AD DS

Scenario
You need to create groups for the Research department. You require a distribution global group to
facilitate email delivery to the Research users. Cai Chu will manage this group. You will also create a
Research Managers group and add Cai Chu and Vera Pace as members of the group. You also need to
create a universal group in the Managers OU that will contain all the departmental managers’ global
groups. After creating the research distribution group, you realize that the group needs access to network
resources, so you must convert the group to a security group.
The main tasks for this exercise are as follows:
1. Create groups and add members.
2. Configure group nesting.
3. Convert a group type from distribution to security

Exercise 1: Creating and managing object in AD DS
    
Task 1: Create groups and add members
1. On LON-DC1, in Server Manager, click Tools, and then click Active Directory Administrative
Center.
2. Click Adatum (local), and then click Managers.
3. In the Tasks pane, under Managers, click New, and then click Group.
4. In the Group name: field, type Enterprise Managers.
5. Under Group scope, click Universal.
6. Click OK to close the Create Group: Enterprise Managers window.
7. Click Adatum (local), and then click the Research organizational unit (OU).
8. In the Tasks pane, under Research, click New, and then click Group.
9. In the Group name: field, type Research Mail.
10. In the Group type section, select Distribution.
11. In the Email field, type Research@adatum.com.
12. In the Managed By section, click Edit.
13. In the Select Users, Contacts, or Groups dialog box, in Enter the object names to select
(examples), type Cai, click Check Names, and then click OK.
20. Select the Manager can update membership list check box.
21. Click OK to close the Create Group: Research Mail window.
22. In the Tasks pane, under Research, click New, and then click Group.
23. In the Group name: field, type Research Managers.
24. Scroll to the Members section, and then click Add.
25. In the Select Users, Contacts, Computers, Service Accounts, or Groups dialog box, in Enter the
object names to select (examples), type Cai click Check Names, and then click OK.
26. Click OK to close the Create Group: Research Managers window.

Task 2: Configure group nesting
1. Double-click Adatum(Local) and then double-click the Managers OU.
2. Right-click the Enterprise Managers group, and then click Properties.
3. In the navigation pane, click Members, and then click Add.
4. In the Select Users, Contacts, Computers, Service Accounts, or Groups dialog box, in Enter the
object names to select (examples), type Managers; Research Managers, click Check Names, and
then click OK.
5. Click OK to close the Enterprise Managers window.
   
Task 3 : Convert a group type from distribution to security
1. In the navigation pane, click Research.
2. Double-click the Research Mail group.
3. Under Group type, click Security, and then click OK.


Exercise 2: Creating and configuring user accounts in AD DS

Scenario
A. Datum Corporation has several scripts that administrators have used in the past to create user accounts
by using command-line tools. However, an enterprise-wide mandate specifies that administrators will use
Windows PowerShell to perform all future scripting. As the first step in creating scripts, you need to identify
the syntax required to manage AD DS objects in Windows PowerShell.
You have a .csv file that contains a large list of new users for the branch office. It is inefficient to create these
users individually with graphical tools, so you will use a Windows PowerShell script instead. A colleague
who has experience with scripting has given you a script that she created. You need to sign in as branch
administrator and modify the script to match the format of your .csv file.
The main tasks for this exercise are as follows:
1. Create a user account by using Windows PowerShell.
2. Create a new group by using Windows PowerShell.
3. Add a member to the group by using Windows PowerShell.
4. Modify the .csv file.
5. Modify the script.
6. Run the script.
7. Prepare for the next module.

Scenario
You have a list of new users that you must create for the branch office. You have decided to create a
template to facilitate the quick creation of users for the branch. You will validate that template by creating a
new test user and checking the properties.
The main tasks for this exercise are as follows:
1. Create and configure a user template for the Research department.
2. Create new users for the Research branch office based on the template.
3. Validate the template

Task 1: Create and configure a user template for the Research department
1. Ensure that the Research OU is selected.
2. In the Tasks pane, under Research, click New, and then click User.
3. In the Create User window, in the First name field, type _Research Template.
4. In the User UPN logon field, type ResearchTemplate.
5. In the Password and Confirm password fields, type Pa55w.rd.
6. In the navigation pane, click Organization, and then in the Department field, type Research.
7. In the Company field, type Adatum.
8. In the Manager field, click Edit.
9. In the Select Users or Contacts dialog box, in Enter the object names to select (examples), type
Cai, click Check Names, and then click OK.
10. In the navigation pane, click Member Of.
11. Click Add.
12. In the Select Groups dialog box, in Enter the object names to select (examples), type Research,
and then click Check Names. In the Multiple Names Found dialog box, select Research, and then
click OK twice.
13. In the navigation pane, click Profile.
14. In the Log on script field, type \\LON-DC1\Netlogon\Logon.bat, and then click OK.
15. Click the _Research Template account, and then in the Tasks pane, under _Research Template, click
Disable.
16. Close Active Directory Administrative Center.
    
Task 2: Create new users for the Research branch office based on the template
1. In Server Manager, click Tools, and then click Active Directory Users and Computers.
2. Expand Adatum.com, and then click the Research OU.
3. Right-click the _Research Template account, and then click Copy.
4. In the Copy Object – User dialog box, type Research in the First name field, and then type User in
the Last name field.
5. In the User logon name field, type ResearchUser, and click Next.
6. In the Password and Confirm password fields, type Pa55w.rd.
7. Clear the Account is disabled check box, and then click Next.
8. Click Finish.

Task 3: Validate the template
1. Double-click Research User.
2.  Click the Organization tab, and then ensure that the Department is Research, the Company is
Adatum, and the Manager is Cai Chu.
3. Click the Member Of tab, and then ensure that the user is a member of the Research group.
4. Click Cancel to close the Research User Properties dialog box.

Exercise 3: Managing computer objects in AD DS

Scenario
A user is unable to sign in, and a workstation has lost its connectivity to the domain and cannot
authenticate users properly. When users attempt to access resources from this workstation, access is denied.
You need to repair the trust relationship between the computer and the domain.
The main tasks for this exercise are as follows:
1. Reset a computer account.
2. Observe the behavior when a client attempts to sign in.
3. Resolve the computer issue.

Task 1: Reset a computer account
1. In Active Directory Users and Computers, click the Computers container.
2. In the details pane, right-click the LON-SVR2 computer account, and then click Reset Account.
3. In the Active Directory Domain Services dialog box, click Yes.
4. In the Active Directory Domain Services message box, click OK.
Task 2: Observe the behavior when a client attempts to sign in
Restart LON-SVR2, and then attempt to sign in as Adatum\Cai with the password Pa55w.rd.

Task 3: Resolve the computer issue
1. Sign in to LON-SVR2 as Administrator with the password Pa55w.rd.
2. Right-click the Start button, and then click Run.
3. Type PowerShell, and then press Enter.
4. In the Administrator: Windows PowerShell window, type the following cmdlet, and then press Enter:
```
Test-ComputerSecureChannel –Repair
```
5. Close the Windows PowerShell window, and then sign out.
6. Sign in as Adatum\Cai with the password Pa55w.rd. The sign in will succeed now.
7. Sign out of LON-SVR2.

Administering AD DS

Scenario
You have been working for the A. Datum Corporation as a desktop support specialist and have performed
troubleshooting tasks on desktop computers to resolve application and network problems. You recently
accepted a promotion to the server support team. One of your first assignments is to configure the
infrastructure service for a new branch office.
To begin the deployment of the new branch office, you are preparing AD DS objects. As part of this
preparation, you need to create an OU for the branch office and delegate permission to manage it. Also,
you need to evaluate Windows PowerShell to manage AD DS more efficiently.
Objectives

After completing this lab, you will have:
Delegated administration for OUs.
Used Windows PowerShell to manage AD DS objects.

Exercise 1: Delegating administration for OUs

Scenario
A. Datum Corporation delegates management of each branch office to a specific group. This allows IT
employees who work onsite to be administrators for the branch. Each branch office has a branch
administrators group that can perform full administration within the branch office OU. There is also a
branch office helpdesk group that can manage users in the branch office OU, but not other objects. You
need to create the OU and these groups for the new branch office and delegate permissions to the groups.
You will also validate the permissions.
The main tasks for this exercise are as follows:
1. Create a new OU for the branch office.
2. Create groups for branch administrators and branch help-desk personnel.
3. Add members to the group.
4. Delegate permissions to the group.
5. Test permissions.

Task 1: Create a new OU for the branch office
1. On LON-DC1, in Active Directory Users and Computers, right-click Adatum.com, click New, and then
click Organizational Unit.
2. In the New Object – Organizational Unit dialog box, type London in the Name field, and then click
OK.

Task 2: Create groups for branch administrators and branch help-desk personnel
1. Right-click the London OU, click New, and then click Group.
2. In the New Object – Group dialog box, type London Admins, and then click OK.
3. Repeat steps 1 and 2 to create a group named London Helpdesk.

Task 3: Add members to the group
1. Click the IT OU.
2. Right-click the Beth Burke user account, and then click Add to a group.
3. In the Select Groups dialog box, in Enter the object names to select (examples):, type London
Admins. Click Check Names, and then click OK.
4. In the Active Directory Domain Services message box, click OK.
5. Right-click the Dante Dabney user account, and then click Add to a group.
6. In the Select Groups dialog box, in Enter the object names to select (example):, type London
Helpdesk. Click Check Names, and then click OK.
7. In the Active Directory Domain Services message box, click OK.

Task 4: Delegate permissions to the group
1. In Active Directory Users and Computers, click View, and then click Advanced Features.
2. Right-click the London OU, and then click Properties.
3. Click the Security tab, and then click Add.
4. In the Select Users, Computers, Service Accounts or Groups dialog box, in Enter the object names
to select (example):, type London Admins. Click Check Names, and then click OK.
5. Ensure that the London Admins group is selected, check Full Control in the Allow column, and then
click OK.
6. Right-click the London OU, and then click Delegate Control.
7. In the Delegation of Control Wizard, click Next.
8. On the Users or Groups page, click Add.
9. In the Select Users, Computers, or Groups dialog box, in Enter the object names to select
(example):, type London Helpdesk. Click Check Names, click OK, and then click Next.
10. On the Tasks to Delegate page, click Create a custom task to delegate, and then click Next.
11. On the Active Directory Object Type page, click Only the following object in this folder.
12. Scroll to the bottom of the list. Click User objects, and then select the check boxes for Create selected
objects in this folder and Delete selected objects in this folder, and then click Next.
13. On the Permissions page, click Full Control, and then click Next.
14. Click Finish.

Task 5: Test permissions
1. Switch to LON-SVR2.
2. Click Start, click Server Manager, and then click Add roles and features.
3. In the Add Roles and Features Wizard, click Next.
4. On the Select installation type page, click Next.
5. On the Select destination server page, click Next.
6. On the Select server roles page, click Next.
7. On the Select features page, expand Remote Server Administration Tools, and then expand Role
Administration Tools. Expand AD DS and AD LDS Tools. Select the check box beside AD DS Tools,
and then click Next.
8. Click Install. Wait for the installation to complete.
9. When the installation is complete, click Close.
10. Sign out of LON-SVR2.

Test permissions for London Admins
1. Sign in to LON-SVR2 as Beth with the password Pa55w.rd.
2. Click Start, and then click the Server Manager tile.
3. Click Tools, and then click Active Directory Users and Computers.
4. Expand Adatum.com, and then click the Research OU. Notice that the icons on the toolbar to create
users, groups, or OUs are dimmed.
5. Click the London OU. Notice that those icons are available now.
6. Right-click the London OU, click New, and then click Organizational Unit.
7. In the New Object – Organizational Unit dialog box, type Laptops in the Name field, and then click
OK. The creation will succeed.
8. Sign out of LON-SVR2.
9. 
Test permissions for London Helpdesk
1. Sign in to LON-SVR2 as Dante with the password Pa55w.rd.
2. Click Start, and then click the Server Manager tile.
3. Click Tools, and then click Active Directory Users and Computers.
4. Expand Adatum.com, and then click the London OU. Notice that the only available icon is the create
user icon.


Exercise 2: Creating and modifying AD DS objects with Windows PowerShell

Task 1: Create a user account by using Windows PowerShell
1. Switch to LON-DC1.
2. Right-click the Start button, and then click Windows PowerShell (Admin).
3. Create a user account for Ty Carlson in the London OU by running the following command:
```
New‐ADUser ‐Name Ty ‐DisplayName "Ty Carlson" ‐GivenName Ty ‐Surname Carlson ‐Path "ou=London,dc=adatum,dc=com"
```
4. Set the password for the account by running the following command:
```
Set-ADAccountPassword Ty
```
5. When you receive a prompt for the current password, press Enter.
6. When you receive a prompt for the desired password, type Pa55w.rd, and then press Enter.
7. When you receive a prompt to repeat the password, type Pa55w.rd, and then press Enter.
8. To enable the account, run the following command:
```
Enable-ADAccount Ty
```
9. Test the account by switching to LON-CL1, and then sign in as Ty with the password Pa55w.rd.

Task 2: Create a new group by using Windows PowerShell
 On LON-DC1, in the Administrator: Windows PowerShell window, run the following command:
```
New‐ADGroup LondonBranchUsers ‐Path "ou=London,dc=adatum,dc=com" ‐GroupScope Global ‐GroupCategory Security
```
Task 3: Add a member to the group by using Windows PowerShell
1. In the Administrator: Windows PowerShell window, run the following command:
Add‐ADGroupMember LondonBranchUsers ‐Members Ty
2. Confirm that the user is in the group by running the following command:
```
Get‐ADGroupMember LondonBranchUsers
```
Task 4: Modify the .csv file
1. On the taskbar, click the File Explorer icon.
2. In File Explorer, expand Allfiles (E:), expand Labfiles, and then click Mod02.
3. Right-click LabUsers.ps1, and then click Edit. In Administrator: Windows PowerShell (ISE), read the
comments at the top of the script, and then identify the requirements for the header in the .csv file.
4. In File Explorer, double-click LabUsers.csv.
5. In the How do you want to open this type of file (.csv)? message, click Notepad. Click OK.
6. In Notepad, type the following line at the top of the file:
FirstName,LastName,Department,DefaultPassword
7. Click File, and then click Save.
8. Close Notepad.

Task 5: Modify the script
1. In the Administrator: Windows PowerShell (ISE) window, under Variables, replace C:\path\file.csv
with E:\Labfiles\Mod02\LabUsers.csv.
2. Under Variables, replace "ou=orgunit,dc=domain,dc=com" with
"ou=London,dc=adatum,dc=com".
3. Click File, and then click Save. Scroll down, and then review the contents of the script.
4. Close the Administrator: Windows PowerShell (ISE) window.

Task 6: Run the script
1. Switch to the Administrator: Windows PowerShell window.
2. At the prompt, type cd E:\Labfiles\Mod02, and then press Enter.
3. Type .\LabUsers.ps1, and then press Enter.
4. To view the users just created, type the following command, and then press Enter:
```
Get‐ADUser ‐Filter * ‐SearchBase "ou=London,dc=adatum,dc=com"
```

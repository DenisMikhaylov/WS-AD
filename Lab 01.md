
Module 2: Advanced Deployment and Administration of  AD DS

Lab: Deploying and Administering AD DS

Exercise 1: Deploying AD DS

Task 1: Install AD DS binaries

1. Switch to LON-DC1.
2. In Server Manager, click Tools, and then click Windows PowerShell.
3. At a command prompt in the Windows PowerShell command-line interface, type the following
command, and then press Enter:
Install-WindowsFeature –Name AD-Domain-Services –ComputerName LON-SVR1
4. Wait after the installation is finished. Type the following command to verify that the Active Directory
Domain Services (AD DS) role is installed on LON-SVR1, and then press Enter:
Get-WindowsFeature –ComputerName LON-SVR1
5. In the output of the previous command, scroll up and search for “Active Directory Domain
Services.” Verify that the check box is selected. Also, search for “Remote Server Administration
Tools.” Look for the Role Administration Tools node below, and then look for the node AD DS and
AD LDS Tools. Note that below that node, only Active Directory module for Windows PowerShell
has been installed, but not the graphical tools like Active Directory Administrative Center. If you
manage your servers centrally, you usually do not need these on each server. If you want to install
them, you need to specify the AD DS tools with RSAT-ADDS.
 Task 2: Prepare the AD DS installation and promote a remote server
Add LON-SVR1 to Server Manager on LON-DC1
1. On LON-DC1, in Server Manager, select the All Servers view.
2. On the top menu, click the Manage menu, and then select Add Servers.
3. In the Add Servers dialog box, maintain the default settings, and then click Find Now.
4. In the Active Directory list of servers, select LON-SVR1, click the arrow to add it to the Selected list,
and then click OK.
Configure AD DS remotely by using Server Manager
1. On LON-DC1, when the installation of the AD DS role on LON-SRV1 is finished and the server is
added to Server Manager, in Server Manager, on the top menu, click the Notifications flag symbol.
2. Note the Post-deployment Configuration of LON-SVR1, and then click the Promote this server to a
domain controller link.
3. In the Active Directory Domain Services Configuration Wizard, on the Deployment Configuration
page, Select the deployment operation to Add a domain controller to an existing domain.
Ensure that the domain Adatum.com is specified. In the Supply the credentials to perform this
operation section, click Change.MCT USE ONLY. STUDENT USE PROHIBITED
L2-4 Advanced Deployment and Administration of AD DS
4. In the Credentials for deployment operation dialog box, enter the following, click OK, and then
click Next:
o User name: Adatum\Administrator
o Password: Pa$$w0rd
5. On the Domain Controller Options page, remove the selections for the Domain Name System
(DNS) server and Global Catalog (GC). Read-only domain controller (RODC) also should not be
selected.
6. In the Type the Directory Services Restore Mode (DSRM) password section, enter and confirm the
password Pa$$w0rd, and then click Next.
7. On the Additional Options page, click Next.
8. On the Paths page, keep the default path settings for the Database folder, Log files folder, and
SYSVOL folder, and then click Next.
9. On the Review Options page, open the generated Windows PowerShell script by clicking View
script.
10. In Notepad, edit the generated Windows PowerShell script:
o Delete comment lines introduced with the number sign (#).
o Remove the Import-Module line.
o Remove the grave accent (`) symbols at the end of each line.
o Remove the line breaks.
11. Now the command Install-ADDSDomainController and all parameters are in one line. Place the
cursor in front of the line, and then press Shift+End to mark the whole line. In the menu, click Edit,
and then click Copy.
12. Switch to the Active Directory Domain Services Configuration Wizard, and then click Cancel. Confirm
with Yes to cancel the wizard.
13. Switch to Server Manager. From the menu, click Tools, and then click Windows PowerShell.
14. At the Windows PowerShell command prompt, type the following command:
Invoke-Command –ComputerName LON-SVR1 { }
15. Place the cursor between the braces, paste the content of the copied script line from the clipboard,
and then press Enter to start the command. The whole line should now be:
Invoke-Command –ComputerName LON-SVR1 { Install-ADDSDomainController –
NoGlobalCatalog:$true –CreateDnsDelegation:$false –Credential (Get-Credential) –
CriticalReplicationOnly:$false –DatabasePath “C:\Windows\NTDS” –DomainName
“Adatum.com” –InstallDns:$false –LogPath “C:\Windows\NTDS” –
NoRebootonCompletion:$false –SiteName “Default-First-Site-Name” –SysvolPath
“C:\Windows\SYSVOL” –Force:$true }
16. In the Windows PowerShell Credential Request dialog box, enter the following, and then click OK:
o User name: Adatum\Administrator
o Password: Pa$$w0rd
17. When prompted, enter and confirm the SafeModeAdministratorPassword as Pa$$w0rd.
18. Wait until the command executes and “Status Success” returns. LON-SVR1 restarts.MCT USE ONLY. STUDENT USE PROHIBITED
Active Directory® Services with Windows Server® L2-5
19. Switch to Notepad, and then close it. When prompted, click Don’t Save.
20. After LON-SVR1 restarts, on LON-DC1, switch to Server Manager, and on the left-hand side, click the
AD DS node. Note that LON-SVR1 has been added as a server and that the warning notification has
disappeared. You might have to click Refresh.
 Task 3: Run the AD DS Best Practices Analyzer
1. On LON-DC1, in Server Manager, go to the AD DS dashboard view.
2. Scroll down to the Best Practices Analyzer section, click the Tasks menu, and then select Start BPA
Scan.
3. In the Select Servers dialog box, select LON-DC1.Adatum.com and LON-SVR1.Adatum.com.
4. Click Start Scan, and then wait until the Best Practices Analyzer (BPA) has finished the scan.
5. Review the results of the BPA.
Exercise 2: Deploying Domain Controllers by Performing Domain
Controller Cloning
 Task 1: Check for domain controller clone prerequisites
1. On LON-DC1, in Server Manager, click Tools, and then click Active Directory Administrative
Center.
2. In Active Directory Administrative Center, double-click Adatum (local), and then in the details pane,
double-click the Domain Controllers organizational unit (OU).
3. In the details pane, select LON-DC1, and then in the Tasks pane, in the LON-DC1 section, click Add
to group.
4. In the Select Groups dialog box, in the Enter the object names to select, type Cloneable, and then
click Check Names.
5. Ensure that the group name is expanded to Cloneable Domain Controllers, and then click OK.
6. On LON-DC1, in the taskbar, click the Windows PowerShell icon.
7. At the Windows PowerShell command prompt, type the following command, and then press Enter:
Get-ADDCCloningExcludedApplicationList
8. Verify the list of critical apps. In production, you would need to verify each app or use a domain
controller that has fewer apps installed by default. Accept the risk, type the following command, and
then press Enter:
Get-ADDCCloningExcludedApplicationList –GenerateXML
9. Now, type the following command to create the DCCloneConfig.xml file, and then press Enter.
New-ADDCCloneConfigFileMCT USE ONLY. STUDENT USE PROHIBITED
L2-6 Advanced Deployment and Administration of AD DS
 Task 2: Copy the source domain controller
1. Type the following command to shut down LON-DC1, and then press Enter:
Stop-Computer
2. On the host computer, in Hyper-V Manager, in the details pane, select the 10969B-LON-DC1 virtual
machine.
3. In the Actions pane, in the 10969B-LON-DC1 section, click Export.
4. In the Export Virtual Machine dialog box, type the location D:\Program Files\Microsoft Learning
\10969, and then click Export.
Note: Depending on your classroom’s setup, the Program Files\Microsoft Learning\10969
folder might be on drive C. Please locate and use the existing folder for the remainder of the lab.
5. Wait until the export finishes.
6. In the Actions pane, in the 10969-LON-DC1 section, click Start, and then sign in as
Adatum\Administrator with password Pa$$w0rd.
 Task 3: Perform domain controller cloning
1. On the host computer, switch to Hyper-V Manager.
2. In the Actions pane, in the upper section that is named for the host computer, click Import Virtual
Machine.
3. In the Import Virtual Machine Wizard, on the Before You Begin page, click Next.
4. On the Locate Folder page, click Browse, select the D:\Program Files\Microsoft Learning\10969
\10969B-LON-DC1 folder, click Select Folder, and then click Next.
5. On the Select Virtual Machine page, select 10969B-LON-DC1, and then click Next.
6. On the Choose Import Type page, select Copy the virtual machine (create a new unique ID), and
then click Next.
7. On the Choose Folders for Virtual Machine Files page, select the Store the virtual machine in
a different location check box. For each folder location, provide the path D:\Program Files
\Microsoft Learning\10969\, and then click Next.
8. On the Choose Folders to Store Virtual Hard Disks page, provide the path D:\Program Files
\Microsoft Learning\10969\, and then click Next.
9. On the Completing Import Wizard page, click Finish.
10. In the details pane, identify and select the newly imported virtual machine 10969B-LON-DC1, which
has the State shown as Off. In the lower section of the Actions pane, click Rename.
11. In the virtual machines pane, in the name column, type 10969B-LON-DC3 as the name, and then
press Enter
12. In the Actions pane, in the 10969-LON-DC3 section, click Start, and then click Connect to start the
machine.
13. While the server is starting, note the “Domain Controller cloning is at x% completion” message.MCT USE ONLY. STUDENT USE PROHIBITED
Active Directory® Services with Windows Server® L2-7
Exercise 3: Administering AD DS
 Task 1: Use Active Directory Administrative Center
Navigate within Active Directory Administrative Center
1. On LON-DC1, in Server Manager, click Tools, and then click Active Directory Administrative
Center.
2. Switch to the tree view, and then expand Adatum (local).
Perform an administrative task within Active Directory Administrative Center
1. In Active Directory Administrative Center, click Overview.
2. In the Reset Password box, in the User name field, type Adatum\Adam.
3. In the Password and Confirm password fields, type Pa$$w0rd.
4. Clear the check box for User must change password at next log on, and then click Apply.
5. In the Global Search section, type Rex in the Search field, and then press Enter.
Create objects
1. In Active Directory Administrative Center, in the Navigation pane, click Adatum (local), and then
click Computers.
2. In the Tasks pane, in the Computers section, click New, and then select Computer.
3. In the Create Computer dialog box, enter the following information, and then click OK:
o Computer name: LON-CL4
o Computer (NetBIOS) name: LON-CL4
View all object attributes
1. In Active Directory Administrative Center, double-click Adatum (local), and then in the details pane,
double-click Computers.
2. Select LON-CL4, and in the Tasks pane, in the LON-CL4 section, click Properties.
3. In the LON-CL4 properties window, scroll down to the Extensions section, click the Attribute Editor
tab, and then note that all attributes of the computer object are available here.
4. Close the LON-CL4 properties window by clicking Cancel.
Use the Windows PowerShell History viewer
1. In Active Directory Administrative Center, click the Windows PowerShell History toolbar at the
bottom of the screen.
2. View the details for the New-ADComputer cmdlet that was used to perform the most recent task.
3. On LON-DC1, close all open windows.
 Task 2: Use Windows PowerShell to administer AD DS
1. On LON-DC1, in Server Manager, click Tools, and then click Active Directory module for Windows
PowerShell.
2. At the Windows PowerShell command prompt, type the following, and then press Enter:
Get-ADUser –filter {Department –eq ‘Marketing’} –properties department | ft
name,departmentMCT USE ONLY. STUDENT USE PROHIBITED
L2-8 Advanced Deployment and Administration of AD DS
3. Verify in the output of the command that all users belong to the Marketing department.
4. At the Windows PowerShell command prompt, type the following, and then press Enter:
Get-ADUser –LDAPFilter “(&(objectClass=User)(department=Marketing))” –properties sn |
where {$_.sn –ge ‘L’} | Set-ADUser –department ‘Marketing2’
5. In Server Manager, click Tools, and then click Active Directory Administrative Center.
6. In Active Directory Administrative Center, double-click Adatum (local), in the details pane, scroll
down, and then double-click Marketing.
7. Confirm that user accounts with a last name beginning with L through Z have the department
Marketing2 in their properties.
8. At the Windows PowerShell command prompt, type the following, and then press Enter:
Get-ADOrganizationalUnit –filter * -Properties ProtectedFromAccidentalDeletion |
where {$_.ProtectedFromAccidentalDeletion –match $False}
9. Verify in the output of the command that the domain controller’s default OU is not protected from
accidental deletion.
10. At the Windows PowerShell command prompt, type the following, and then press Enter:
Get-ADOrganizationalUnit –filter * -Properties ProtectedFromAccidentalDeletion |
where {$_.ProtectedFromAccidentalDeletion –match $False} | Set-ADOrganizationalUnit –
ProtectedFromAccidentalDeletion $true
11. At the Windows PowerShell command prompt, type the following, and then press Enter:
Get-ADOrganizationalUnit –filter * -Properties ProtectedFromAccidentalDeletion |
where {$_.ProtectedFromAccidentalDeletion –match $False}
12. Verify that the domain controller’s OU is no longer listed. The results are empty because the domain
controller’s OU is now protected from accidental deletion.
 Prepare for the next module
When you have completed the lab, revert the virtual machines back to their initial state. To do this,
complete the following steps:
1. On the host computer, start Hyper-V Manager.
2. Right-click 10969B-LON-DC3, and then click Turn Off.
3. In the Turn Off Machine dialog box, click Turn Off.
4. Right-click 10969B-LON-DC3, then click Delete.
5. In the Delete Selected Virtual Machines dialog box, click Delete.
6. In the Virtual Machines list, right-click 10969B-LON-DC1, and then click Revert.
7. In the Revert Virtual Machine dialog box, click Revert.
8. Repeat steps six and seven for 10969B-LON-SVR1.

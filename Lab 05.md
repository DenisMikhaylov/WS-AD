Scenario
Your manager asked you to use Group Policy to implement standardized security settings to lock computer
screens when users leave computers unattended for 10 minutes or more. You also have to configure a
policy setting that will prevent access to certain programs on local computers.
You configured Group Policy to lock computer screens when users leave computers unattended for 10
minutes or more. However, after some time, you were made aware that a critical application used by the
Research engineering team fails when the screen saver starts. An engineer asked you to prevent the GPO
setting from applying to any member of the Research security group. He also asked you to configure
conference room computers to be exempt from corporate policy. However, you must ensure that the
conference room computers use a 2-hour time out.
Create the policies that you need to evaluate the RSoPs for users in your environment. Make sure to
optimize the Group Policy infrastructure and verify that all policies are applied as they were intended.
Objectives
After completing this lab, you will be able to:
Create and configure GPOs.
Manage GPO scope.

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
New-ADUser -City:"London" -Company:"Adatum" -Department:"Research" -DisplayName:"Connie Chu" -GivenName:"Connie" -Surname:"Chu" -Name:"Connie Chu" -UserPrincipalName:"Connie@ADATUM.COM" -SamAccountName:"Connie" -Path:"OU=Research,DC=ADATUM,DC=COM"  -Server:"LON-DC1.ADATUM.COM"  -Type:"user" -AccountPassword $password -Enabled $true
```
Exercise 1: Creating and configuring GPOs

Task 1: Create and edit a GPO
1. On LON-DC1, from Server Manager, click Tools, and then click Group Policy Management.
2. If necessary, switch to the Group Policy Management window.
3. In Group Policy Management Console, in the navigation pane, expand Forest: Adatum.com,
Domains, and Adatum.com, and then click the Group Policy Objects container.
4. In the navigation pane, right-click the Group Policy Objects container, and then click New.
5. In the Name text box, type ADATUM Standards, and then click OK.
6. In the details pane, right-click the ADATUM Standards Group Policy Object (GPO), and then click Edit.
7. In the Group Policy Management Editor window, in the navigation pane, expand User
Configuration, expand Policies, expand Administrative Templates, and then click System.
8. Double-click the Prevent access to registry editing tools policy setting.
9. In the Prevent access to registry editing tools dialog box, click Enabled, and then click OK.
10. In the navigation pane, expand User Configuration, expand Policies, expand Administrative
Templates, expand Control Panel, and then click Personalization.
11. In the details pane, double-click the Screen saver timeout policy setting.
12. In the Screen saver timeout dialog box, click Enabled, in the Seconds text box, type 600, and then
click OK.
13. Double-click the Password protect the screen saver policy setting.
14. In the Password protect the screen saver dialog box, click Enabled, and then click OK.
15. Close the Group Policy Management Editor window.

Task 2: Link the GPO
1. In the Group Policy Management window, in the navigation pane, right-click the Adatum.com
domain, and then click Link an Existing GPO.
2. In the Select GPO dialog box, click ADATUM Standards, and then click OK.

Task 3: View the effects of the GPO’s settings
1. Switch to LON-SVR2, and then sign in as Adatum\Administrator with the password Pa55w.rd.
2. Right-click Start, and then click Control Panel.
3. Click System and Security, and then click Allow an app through Windows Firewall.
4. In the Allowed apps and features list, select the following check boxes, and then click OK:
o Remote Event Log Management
o Windows Management Instrumentation (WMI)
5. Sign out, and then sign in as Adatum\Connie with the password Pa55w.rd.
6. Click Start, type screen saver, and then click Change screen saver. (It may take a few minutes for the
option to appear.)
7. In the Screen Saver Settings dialog box, notice that the Wait option is dimmed—you cannot change
the time-out. Notice that the On resume, display logon screen option is selected and dimmed and
that you cannot change the settings. If the On resume, display logon screen option is not selected
and dimmed, then perform the following steps:
a. Right-click Start and then click Run.
b. In the Run dialog box, in the Open text box, type gpupdate /force, and then click OK.
c. Click Start, type screen saver, and then click Change screen saver.
d. Click OK.
e. Right-click Start, and then click Run.
f. In the Run dialog box, in the Open text box, type regedit, and then click OK.
g. In the Registry Editor dialog box, click OK.
Results: After completing this exercise, you should have created, edited, and linked the required GPO
successfully.

Exercise 2: Managing GPO scope
Task 1: Create and link the required GPOs
1. On LON-DC1, in Group Policy Management Console, in the navigation pane, if necessary, expand
Forest: Adatum.com, expand Domains, expand Adatum.com, and then click Research.
2. Right-click the Research organizational unit (OU), and then click Create a GPO in this domain, and
Link it here.
3. In the New GPO dialog box, in the Name text box, type Research Application Override, and then
click OK.
4. In the details pane, right-click the Research Application Override GPO, and then click Edit.
5. In the console tree, expand User Configuration, expand Policies, expand Administrative Templates,
expand Control Panel, and then click Personalization.
6. Double-click the Screen saver timeout policy setting.
7. Click Disabled, and then click OK.
8. Close the Group Policy Management Editor window.

Task 2: Verify the order of precedence
 In the Group Policy Management Console tree, click the Research OU, and then click the Group Policy
Inheritance tab. Notice that the Research Application Override GPO has higher precedence than the
ADATUM Standards GPO. The screen saver time-out policy setting that you just configured in the
Research Application Override GPO is applied after the setting in the ADATUM Standards GPO.
Therefore, the new setting will overwrite the standards setting and will prevail. Screen saver time-out
will be unavailable for users within the scope of the Research Application Override GPO.

Task 3: Configure the scope of a GPO with security filtering
1. On LON-DC1, in Group Policy Management Console, in the navigation pane, if necessary, expand
the Research OU, and then click the Research Application Override GPO under the Research OU.
2. In the Group Policy Management Console dialog box, read the message, select the Do not show
this message again check box, and then click OK.
3. In the Security Filtering section, you will see that the GPO applies by default to all authenticated users.
4. In the Security Filtering section, click Authenticated Users, and then click Remove.
5. In the Group Policy Management dialog box, click OK.
6. In the details pane, click Add.
7. In the Select User, Computer, or Group dialog box, in the Enter the object name to select
(examples): text box, type Research, and then click OK.
8. In the details pane, under Security Filtering, click Add.
9. In the Select User, Computer, or Group dialog box, click Object Types.
10. In the Object Types dialog box, select the Computers check box and then click OK.
11. In the Select User, Computer, or Group dialog box, in the Enter Object Names to select (Examples)
text box, type LON-SVR2, and then click OK.
 

Task 4: Configure loopback processing
1. On LON-DC1, in Group Policy Management Console, in the navigation pane, click Adatum.com,
right-click Adatum.com, and then click New Organizational Unit.
2. In the New Organizational Unit dialog box, in the Name text box, type Kiosks, and then click OK.
3. Right-click Kiosks, and then click New Organizational Unit.
4. In the New Organizational Unit dialog box, in the Name text box, type Conference Rooms, and then
click OK.
5. In the navigation pane, expand the Kiosks OU, and then click the Conference Rooms OU.
6. Right-click the Conference Rooms OU, and then click Create a GPO in this domain, and Link
it here.
7. In the New GPO dialog box, in the Name text box, type Conference Room Settings, and then
click OK.
8. In the navigation pane, expand Conference Rooms, and then click the Conference Room
Settings GPO.
9. In the navigation pane, right-click the Conference Room Settings GPO, and then click Edit.
10. In the Group Policy Management Editor window, in the navigation pane, expand User
Configuration, expand Policies, expand Administrative Templates, expand Control Panel, and then
click Personalization.
11. In the details pane, double-click the Screen saver timeout policy setting, and then click Enabled.
12. In the Seconds text box, type 7200, and then click OK
13. In the navigation pane, expand Computer Configuration, expand Policies, expand Administrative
Templates, expand System, and then click Group Policy.
14. In the details pane, double-click the Configure user Group Policy loopback processing mode policy
setting, and then click Enabled.
15. In the Mode drop-down list, select Merge, and then click OK.
16. Close the Group Policy Management Editor window

Exercise 1: Verifying GPO application

 Task 1: Perform RSoP analysis
1. Switch to LON-SVR2, and then verify that you are signed in as Adatum\Connie. If necessary, use the
password Pa55w.rd.
2. Click Start, type cmd, and then press Enter.
3. At the command prompt, type the following command, and then press Enter:
gpupdate /force
4. Wait for the command to complete. Make a note of the current system time, which you will need to
know for a task later in this lab. To record the system time, type the following command, and then
press Enter twice:
Time
5. Restart LON-SVR2. Wait for LON-SVR2 to restart before proceeding with the next task. Do not sign in to
LON-SVR2.
6. Switch to LON-DC1.
7. Switch to Group Policy Management Console.
8. In the navigation pane, if necessary, expand Forest: Adatum.com, and then click Group Policy
Results.
9. Right-click Group Policy Results, and then click Group Policy Results Wizard.
10. On the Welcome to the Group Policy Results Wizard page, click Next.
11. On the Computer Selection page, select the Another computer option, type LON-SVR2, and then
click Next.
12. On the User Selection page, click ADATUM\Connie, and then click Next.
13. On the Summary of Selections page, review your settings, and then click Next.
14. Click Finish. The RSoP report appears in the details pane of Group Policy Management Console.
15. Review the summary results. For both the user and the computer configuration, identify the time of the
last policy refresh and the list of allowed and denied GPOs. Identify the components that were used to
process policy settings.
16. Click the Details tab. Review the settings that were applied during user and computer policy
application, and then identify the GPO from which the settings were obtained.
17. Click the Policy Events tab, and then locate the event that logs the policy refresh that you triggered
with the gpupdate command.
18. Click the Summary tab, right-click an empty space on the page, and then click Save Report.
19. In the navigation pane, click Desktop, and then click Save.MCT USE ONLY. STUDENT USE PROHIBITED
L5-36 Implementing Group Policy
20. On the desktop, right-click Connie on LON-SVR2.htm, point to Open with, and then click Internet
Explorer.
21. When you have examined the report, close Microsoft Internet Explorer.

Task 2: Analyze RSoP with GPResult
1. Sign in to LON-SVR2 as Adatum\Connie with the password Pa55w.rd.
2. Right-click Start, and then click Command Prompt.
3. At the command prompt, type the following command, and then press Enter:
gpresult /r
4. RSoP summary results are displayed. Notice that the information is very similar to the Summary tab of
the RSoP report that was produced by Group Policy Results Wizard.
5. At the command prompt, type the following command, and then press Enter:
gpresult /v | more
6. Press the spacebar to proceed through the report. Notice that many of the Group Policy settings that
were applied by the client are listed in this report.
7. At the command prompt, type the following command, and then press Enter:
gpresult /z | more
8. Press the spacebar to proceed through the report. This is the most detailed RSoP report.
9. At the command prompt, type the following command, and then press Enter:
gpresult /h:"%userprofile%\Desktop\RSOP.html"
An RSoP report is saved as an HTML file to your desktop.
10. Open the saved RSoP report from your desktop. Compare the report, its information, and its
formatting with the RSoP report that you saved in the previous task.
11. Sign out of LON-SVR2.

Task 3: Evaluate GPO results by using Group Policy Modeling Wizard
1. On LON-DC1, in Group Policy Management Console, in the navigation pane, click Group Policy
Modeling.
2. Right-click Group Policy Modeling, and then click Group Policy Modeling Wizard.
3. In the Group Policy Modeling Wizard, click Next.
4. On the Domain Controller Selection page, click Next.
5. On the User and Computer Selection page, in the User information section, select the User option,
and then click Browse. In the Select User dialog box type Connie, and then press Enter.
6. In the Computer information section, select the Computer option, and then click Browse. In the
Select Computer dialog box, type LON-SVR2, and then press Enter.
7. In the Group Policy Modeling Wizard, click Next.MCT USE ONLY. STUDENT USE PROHIBITED
Identity with Windows Server 2016 L5-37
8. On the Advanced Simulation Options page, select the Loopback Processing check box, and then
select the Merge option. Even though the Conference Room Settings GPO specifies loopback
processing, you must instruct Group Policy Modeling Wizard to consider loopback processing in its
simulation. Click Next.
9. On the Alternate Active Directory Paths page, next to Computer location, click Browse.
10. In the Choose Computer Container dialog box, expand Adatum, expand Kiosks, and then click
Conference Rooms. You are simulating the effect of LON-SVR2 as a conference room computer. Click
OK, and then click Next.
11. On the User Security Groups page, click Next.
12. On the Computer Security Groups page, click Next.
13. On the WMI Filters for Users page, click Next.
14. On the WMI Filters for Computers page, click Next.
15. Review your settings on the Summary of Selections page, click Next, and then click Finish.
16. In the details pane, click the Details tab, if necessary expand User Details, expand Group Policy
Objects, and then expand Applied GPOs.
17. Verify if the Conference Room Settings GPO applies to Connie as a User policy when she signs in to
LON-SVR2, if LON-SVR2 is in the Conference Rooms OU.
18. Scroll to, and if necessary expand, User Details, expand Settings, expand Policies, expand
Administrative Templates, and then expand Control Panel/Personalization.
19. Confirm that the screen saver timeout is 7,200 seconds (2 hours)—the setting configured by the
Conference Room Settings GPO that overrides the 10-minute standard configured by the ADATUM
Standards GPO.

Task 4: Review policy events
1. Switch to LON-SVR2. Sign in as Adatum\Administrator with the password Pa55w.rd.
2. Right-click Start, and then click Event Viewer.
3. In the navigation pane, expand Windows Logs, and then click the System log.
4. Click the Source column header to sort the System log by source.
5. Locate event 1500, 1501, 1502, or 1503 with Group Policy as the source.
6. Review the information that is associated with Group Policy events.
7. In the navigation pane, expand Applications and Services Logs, expand Microsoft, expand
Windows, expand Group Policy, and then click Operational.
8. Locate the first event related to the Group Policy refresh that you initiated in the first exercise with the
gpupdate command. Review that event and the events that followed it.
9. Sign out of LON-SVR2.
Results: After completing this exercise, you should have used the RSoP tools successfully to verify the
correct application of your GPOs, examined Group Policy events, and verified the health of the Group Policy
infrastructure.

Exercise 2: Troubleshooting GPOs

Task 1: Read the Help desk Incident Record and simulate the problem
1. Read Help desk Incident Record 604531 in the exercise scenario.
2. On LON-DC1, on the taskbar, click File Explorer.
3. In File Explorer, in the navigation pane, expand Allfiles (E:), expand Labfiles, and then click Mod05.
4. In the details pane, right-click Mod05-1.ps1, and then click Run with PowerShell. If prompted, press Y
and then press Enter.
 Task 2: Update the Plan of Action section of the Incident Record
1. Read the Additional Information section of the Incident Record in the exercise scenario in the
student manual.
2. Update the Plan of Action section of the Incident Record in the student manual with your
recommendations:
o Verify the configuration for Connie Vaughn.
o RSoP from Group Policy Results Wizard will afterward provide the configuration information for
Connie Vaughn.
o The Research Application Override GPO should provide the correct configuration. Investigate
the configuration of the GPO.
 Task 3: Troubleshoot and resolve the problem
1. On LON-SVR2, sign in as Adatum\Connie with the password Pa55w.rd.
2. Right-click Start, and then click Control Panel.
3. In Control Panel, click Appearance and Personalization, and then click Change Screen Saver.
4. Verify that Wait is dimmed and has a value of 10 minutes.
5. Sign out of LON-SVR2.
6. Switch to LON-DC1.
7. In the Group Policy Management window, in the navigation pane, click Group Policy Results.
8. Right-click Group Policy Results, and then click Group Policy Results Wizard.
9. On the Welcome to the Group Policy Results Wizard page, click Next.
10. On the Computer Selection page, select the Another computer option, type LON-SVR2, and then
click Next.
11. On the User Selection page, click ADATUM\Connie, and then click Next.
12. On the Summary of Selections page, review your settings, and then click Next.
13. Click Finish.
14. Click the Details tab, and then click Show all.
15. In the User Details section, locate the Settings section, and then in Control Panel/Personalization,
verify that the screen saver timeout is 600 seconds and the winning GPO is ADATUM Standards.
16. In the User Details section, locate the denied GPOs and verify that the Research Application
Override GPO is in the list of denied GPOs with a reason of Disabled Link. In this case, it appears that
the GPO link for the Research OU is disabled.
17. In the navigation pane, click the Research OU, right-click the Research OU, and then click Refresh.
18. Expand the Research OU.
19. Notice that the link for the Research Application Override GPO is disabed. In the navigation pane,
right-click the Research Application Override GPO, and then click Link Enabled.
20. Switch to LON-SVR2.
21. On LON-SVR2, sign in as Adatum\Connie with the password Pa55w.rd.
22. Right-click Start, and then click Control Panel.
23. In Control Panel, click Appearance and Personalization, and then click Change Screen Saver.
24. Verify that Wait is no longer dimmed and has a value of 1 minutes.
25. If Wait is still dimmed, then perform the following steps:
a. Right-click Start, hover over Shut down or sign out and then click Restart.
b. Sign in as Adatum\Connie with the password Pa55w.rd.
26. Perform steps 22-24.
27. Sign out of LON-SRV2.
Results: After completing this exercise, you will have resolved the GPO application problem.

Task 4: Prepare for the next module
When you finish the lab, revert the virtual machines to their initial state. To do this, perform the following
steps:
1. On the host computer, start Hyper-V Manager.
2. In the Virtual Machines list, right-click LON-DC1, and then click Revert.
3. In the Revert Virtual Machine dialog box, click Revert.
4. Repeat steps 2 and 3 for LON-SVR2

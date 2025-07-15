Securing AD DS

Scenario

The security team at A. Datum Corporation has been examining possible security issues in the organization,
focusing on AD DS. The security team is particularly concerned with AD DS authentication and security of
branch-office domain controllers.

You must help improve security and monitoring of authentication against the enterprise’s AD DS domain.
Additionally, management at A. Datum has instituted a password policy, and you must enforce it for all user
accounts and develop a more-stringent password policy for security-sensitive administrative accounts. It
also is important that you implement an appropriate audit trail to help monitor authentication attempts
within AD DS.

The second part of your assignment includes deploying and configuring RODCs to support AD DS
authentication within a branch office. Lastly, you should evaluate the usage of a group MSA by deploying it
to the test server.
Objectives

After completing this lab, you will be able to:
Implement security policies for accounts, passwords, and administrative groups.
Deploy and configure an RODC.
Create and associate a group MSA.

Virtual machines: 20742B-LON-DC1 and 20742B-LON-SVR1
User name: Adatum\Administrator
Password: Pa55w.rd


Exercise 1: Implementing security policies for accounts, passwords, and
administrative groups

Scenario

A. Datum management has indicated that it is important that all management processes are as secure as
possible, to help prevent a security breach. The company’s security and management teams have identified
its business requirements with respect to account logons and password security. In this exercise, you will
define and implement the Group Policy settings to meet the company’s requirements.

Supporting documentation
A. Datum GPO strategy proposal

Requirements overview

A. Datum has identified the following requirements regarding account logon and password policies:
 All users must use a password that is at least eight characters long. For IT administrators, the minimum
length must be 10 characters.
 Passwords for all users must be complex and stored securely.
 All users, except IT administrators, must change their password every 60 days or less.
 IT administrators must change their password every 30 days or less.
 If users enter the wrong password more than five times within 20 minutes, their accounts must be locked.
For normal users, accounts are unlocked automatically after one hour.
 For IT administrators, accounts must be locked after three incorrect password attempts. IT administrator
accounts are never unlocked automatically. An administrator must unlock the account. IT administrator
accounts include all members of the IT group and the Domain Admins group.
 No users should be able to use at least 10 of their previous passwords.
 The membership list for the local Administrators group on all member servers must be limited to only the
local Administrator account, the Domain Admins group, and the IT group.
 The Domain Admins group must include only the Administrator account.
 The Enterprise Admins and Schema Admins groups must be empty during normal operations. Users must
be added explicitly to these groups only when they need to perform tasks that require this level of
administrative rights.
 Other built-in groups, such as Account Operators and Server Operators, should contain no members. If
users are added to one of these groups, they should be removed from the group automatically.
All changes made to user objects and security groups in AD DS must be audited.


Proposals
List the settings that you must configure to meet A. Datum’s requirements regarding password policies and
account lockout.

Setting                                    | Configuration for all users | Configuration for IT administrators

Enforce password history
Maximum password age
Minimum password age
Minimum password length
Passwords must meet complexity requirements
Store password using reversible encryption
Account lockout duration
Account lockout threshold
Reset account lockout counter after


1. How can you configure that IT administrators have different password and account lockout settings than
regular users?
2. How can you identify IT administrators in terms of more restricted password and account lockout
settings?
3. How can you meet the requirement to limit the membership list for the local Administrators groups on all
member servers to only the local Administrator account, the Domain Admins group, and the IT group?
4. How can you meet the requirement that the Domain Admins group must include only the Administrator
account, and that the Enterprise Admins and Schema Admins groups must be empty during normal
operations?
5. How can you meet the requirement that other built-in groups, such as Account Operators and Server
Operators, must not contain members?
6. How can you meet the requirement that you must audit all changes to AD DS?


The main tasks for this exercise are as follows:
1. Identify the required settings.
2. Configure password settings for all users.
3. Configure a PSO for IT administrators.
4. Implement administrative security policies.
5. Implement administrative auditing.

Task 2: Configure password settings for all users
1. On LON-DC1, from Server Manager, click Tools, and then click Group Policy Management.
2. In the Group Policy Management console, in the navigation pane, expand Forest:
Adatum.com\Domains\ Adatum.com\Group Policy Objects, and then select the Default Domain
Policy.
3. Right-click Default Domain Policy, and then click Edit.
4. In the Group Policy Management Editor window, in the navigation pane, expand
Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies, and
then double-click Password Policy.
5. In the details pane, double-click Enforce password history.
6. In the Enforce password history Properties dialog box, ensure that Define this policy setting is
selected.
7. Configure Keep password history for: to 10 passwords remembered, click OK, and then doubleclick Maximum password age.
8. In the Maximum password age Properties dialog box, ensure that Define this policy setting is
selected.
9. Configure Password will expire in to 60 days, click OK, and then double-click Minimum
password age.
10. In the Minimum password age Properties dialog box, ensure that Define this policy setting is
selected.
11. Configure Password can be changed after to 1 days, click OK, and then double-click Minimum
password length.
12. In the Minimum password length Properties dialog box, ensure that Define this policy setting is
selected.
13. Configure Password must be at least to 8 characters, click OK, and then double-click Password
must meet complexity requirements.
14. In the Password must meet complexity requirements Properties dialog box, ensure that Define
this policy setting is selected.
15. Select Enabled, click OK, and then double-click Store passwords using reversible encryption.
16. In the Store passwords using reversible encryption Properties dialog box, ensure that Define this
policy setting is selected.
17. Select Disabled, and then click OK.
18. In the navigation pane, click to select Account Lockout Policy.
19. In the details pane, double-click Account lockout duration.
20. In the Account lockout duration Properties dialog box, click Define this policy setting.
21. Configure Account is locked out for to 60 minutes, and then click OK.
22. In the Suggested Value Changes dialog box, click OK, and then double-click Account lockout
threshold.
23. In the Account lockout threshold Properties dialog box, configure Account will lock out after to
5 invalid logon attempts, click OK, and then double-click Reset account lockout counter after.
24. In the Reset account lockout counter after Properties dialog box, configure Reset account lockout
counter after to 20 minutes, and then click OK.
25. Close the Group Policy Management Editor window and the Group Policy Management console.

Task 3: Configure a PSO for IT administrators
1. On LON-DC1, from Server Manager, click Tools, and then click Active Directory Administrative
Center.
2. In Active Directory Administrative Center, in the navigation pane, click Adatum (local).
3. In the details pane, scroll to and double-click System, and then double-click Password Settings
Container.
4. In the Tasks pane, in the Password Settings Container section, click New, and then click Password Settings.
5. In the Create Password Settings dialog box, in the Password Settings section, in the Name field,
type Adatum Administrators Password Settings.
6. In the Precedence field, type 10, and then ensure that Enforce minimum password length is selected.
7. In the Minimum password length (characters) text box, type 10, and then ensure that Enforce
password history is selected.
8. In the Number of passwords remembered text box, type 10, ensure that Password must meet
complexity requirements is selected, and then ensure that Store password using reversible
encryption is not selected.
9. Under Password age options, ensure that Enforce minimum password age is selected.
10. In the User cannot change the password within (days) text box, type 1, and then ensure that the
Enforce maximum password age check box is selected.
11. In the User must change the password after (days) text box, type 30, and then select the Enforce
account lockout policy check box.
12. In the Number of failed logon attempts allowed text box, type 3.
13. In the Reset failed logon attempts count after (mins) text box, type 20, and then select Account
will be locked out, Until an administrator manually unlocks the account.
14. In the Directly Applies To section, click Add.
15. In the Select Users or Groups dialog box, under Enter the object names to select, type IT, and then
click Check Names.
16. The Name Not Found dialog box appears because IT is not a global group but a Universal Group. Click
Cancel.
17. Switch to Server Manager, click Tools, and then click Windows PowerShell.
18. At the Windows PowerShell command prompt, type the following command, and then press Enter:
Get-ADGroup IT
19. Verify that the IT group has a group scope of Universal.
20. At the command prompt, type the following command, and then press Enter:
Set-ADGroup IT –GroupScope Global
21. Switch back to the Create Password Settings: Adatum Administrative Password Settings
dialog box.
22. In the Select Users or Groups dialog box, under Enter the object names to select, type IT; Domain
Admins, and then click Check Names. The names are both resolved. Click OK.
23. Click OK to close the Create Password Settings: Adatum Administrative Password Settings dialog
box and create the Password Settings object (PSO).
24. In Active Directory Administrative Center, in the navigation pane, click Overview.
25. In the details pane, in the Global Search box, type Abbi Skinner, and then press Enter. The user object
of Abbi Skinner is found.
26. In the Tasks pane, click View resultant password settings. Note that the Adatum Administrative
Password Settings PSO applies (Abbi is in the IT group), and then click Cancel.
27. In the Global Search box, type Adam Hobbs, and then press Enter.
28. In the Tasks pane, click View resultant password settings. Note that no resultant fine- grained
password settings apply (Adam is not in the IT group and the Default Domain Policies settings apply to
him), and then click OK.
29. Close Active Directory Administrative Center and Windows PowerShell.


Task 4: Implement administrative security policies

1. On LON-DC1, from Server Manager, click Tools, and then click Active Directory Administrative
Center.
2. In Active Directory Administrative Center, in the navigation pane, click Adatum (local).
3. In the Tasks pane, in the Adatum (local) section, click New, and then click Organizational Unit.
4. In the Create Organizational Unit dialog box, in the Name field, type Adatum Servers, and then
click OK.
5. In Active Directory Administrative Center, in the details pane, double-click Computers, select
LON-SVR1, and then press and hold the Shift key and click LON-SVR2. Both servers now are selected.
6. In the Tasks pane, in the 2 items selected section, click Move.
7. In the Move dialog box, select Adatum Servers, and then click OK.
8. Close Active Directory Administrative Center.
9. In Server Manager, click Tools, and then click Group Policy Management.
10. In the Group Policy Management console, under Forests: Adatum.com\Domains\Adatum.com,
locate and click to select Adatum Servers. Right-click Adatum Servers, and then click Create a GPO
in this domain, and Link it here.
11. In the New GPO dialog box, in the Name field, type Restricted Administrators on Member Servers,
and then click OK.
12. In the details pane, right-click the Restricted Administrators on Member Servers GPO, and then
click Edit.
13. In the Group Policy Management Editor window, expand Computer Configuration\Policies
\Windows Settings\Security Settings, click to select Restricted Groups, right-click Restricted
Groups, and then click Add Group.
14. In the Add Group dialog box, in the Group field, type Administrators, and then click OK.
15. In the Administrators Properties dialog box, under Members of this group, click Add.
16. In the Add Member dialog box, click Browse.
17. In the Select Users, Service Accounts or Groups dialog box, in the Enter the object names to select
text box, type Domain Admins; IT, click Check Names, and then click OK.
18. In the Add Member dialog box, in the Members of this group section, add ;Administrator to the
string, and then click OK.
19. Verify that the Administrator Properties dialog box now shows the following in Members of this
group, and then click OK:
o ADATUM\Domain Admins
o ADATUM\IT
o Administrator
20. Close the Group Policy Management Editor window.
21. On LON-SVR1, click Start, type cmd, and then click Command Prompt.
22. In the Administrator: Command Prompt window, type the following command, and then press
Enter:
gpupdate /force
23. Wait until the command updates the Computer Policy and the User Policy.
24. On LON-SVR1, click Start, and then click Server Manager.
25. From Server Manager, click Tools, and then click Computer Management.
26. In Computer Management, expand System Tools\Local Users and Groups, and then click Groups.
27. Double-click Administrators, and then verify that ADATUM\Domain Admins, ADATUM\IT, and the
local Administrator are members of this group.
28. Close all open windows except for Server Manager.
29. Switch back to LON-DC1, and then switch to Group Policy Management.
30. In the Group Policy Management console, expand Domain Controllers, right-click the Default
Domain Controllers Policy link, and then click Edit.
31. In the Group Policy Management Editor window, expand Computer Configuration\Policies
\Windows Settings\Security Settings, click to select Restricted Groups, right-click Restricted
Groups, and then click Add Group.
32. In the Add Group dialog box, in the Group field, type Server Operators, and then click OK.
33. In the Server Operators Properties dialog box, keep the default settings of This group should
contain no members, and then click OK.
34. Repeat the steps 30 to 33 for the Account Operators group.
35. Close the Group Policy Management Editor window and the Group Policy Management console.


Task 5: Implement administrative auditing
1. On LON-DC1, from Server Manager, click Tools, and then click Group Policy Management.
2. In the Group Policy Management console, expand Forest: Adatum.com\Domains,
Adatum.com\Group Policy Objects, select the Default Domain Controllers Policy, right-click
Default Domain Controllers Policy, and then click Edit.
3. In the Group Policy Management Editor window, expand Computer Configuration\Policies
\Windows Settings\Security Settings\Advanced Audit Policy Configuration\Audit Policies, and
then click to select DS Access.
4. In the details pane, double-click Audit Directory Services Changes.
5. In the Audit Directory Services Changes Properties dialog box, select Configure the following
audit events, select the Success check box, and then click OK.
6. In the navigation pane, navigate to Computer Configuration\Policies\Windows Settings
\Security Settings\Advanced Audit Policy Configuration\Audit Policies, and then click to select
Account Management.
7. In the details pane, double-click Audit Security Group Management.
8. In the Audit Security Group Management Properties dialog box, select Configure the following
audit events, select the Success check box, and then click OK.
9. In the navigation pane, navigate to Computer Configuration\Policies\Windows Settings
\Security Settings\Local Policies, click to select Security Options, and then double-click the
Audit: Force audit policy subcategory settings (Windows Vista or later) to override audit policy
category settings.
10. In the Audit: Force audit policy subcategory settings (Windows Vista or later) to override audit
policy category settings dialog box, select Define this policy setting, ensure that Enabled is
selected, and then click OK.
11. Close the Group Policy Management Editor window and the Group Policy Management console.
12. On LON-DC1, from Start screen, type cmd, and then click Command Prompt.
13. In the Administrator: Command Prompt window, type the following command, and then press
Enter:
gpupdate /force
14. From Server Manager, click Tools, and then click Active Directory Users and Computers.
15. In Active Directory Users and Computers, from the View menu, enable the Advanced Features
view.
16. In the navigation pane, click to select Adatum.com, right-click Adatum.com, and then click
Properties.
17. In the Adatum.com Properties dialog box, on the Security tab, click Advanced.
18. In the Advanced Security Settings for Adatum dialog box, on the Auditing tab, double-click the
Success auditing entry for Everyone with Special access, which applies to This object only.
19. In the Auditing Entry for Adatum dialog box, in the Applies to drop-down list box, select This
object and all descendent objects.
20. Click OK three times to close all open dialog boxes.
21. In Active Directory Users and Computers, in the navigation pane, if necessary, expand
Adatum.com, and then click to select Users.
22. In the details pane, double-click Domain Admins.
23. In the Domain Admins Properties dialog box, click the Members tab, and then click Add.
24. In the Select Users, Contacts, Computers, Service Accounts, or Groups dialog box, in the Enter the
object names to select text box, type Abbi, click Check Names, select Abbi Skinner and then click
OK three times.
25. In Active Directory Users and Computers, in the navigation pane, click to select Marketing.
26. In the details pane, double-click Ada Russel.
27. In the Ada Russel Properties dialog box, on the Address tab, in the City text box, select London, type
Birmingham, and then click OK.
28. Close Active Directory Users and Computers.
29. In Server Manager, click Tools, and then click Event Viewer.
30. In Event Viewer, expand Windows Logs, and then click Security.
31. In the details pane, search for the most recent Event ID 4728, and then double-click the event.
32. In the Event Properties – Event 4728, Microsoft Windows security auditing dialog box, you get the
message “A member was added to a security-enabled global group.” You can see that
ADATUM\Administrator invoked the change and that ADATUM\Abbi was added to the
ADATUM\Domain Admins group.
33. In Event Viewer, in the Windows Logs\Security Log node, search for the two most recent Event IDs
5136, then double-click the older of the two events.
34. In the Event Properties – Event 5136, Microsoft Windows security auditing dialog box, you will see
the following message: “A directory service object was modified.” You can see that
ADATUM\Administrator has modified the user object cn=Ada Russel, and then deleted the London
value. On the right side of the dialog box, click the Up Arrow to move to the next event.
Note: In the Event Properties details page, notice that ADATUM\Administrator modified
Ada Russel and added the Birmingham value.
35. Close all open windows except for Server Manager.
Results: After this exercise, you should have identified and configured the security policies for A. Datum.


Exercise 2: Deploying and configuring an RODC

Task 1: Stage a delegated installation of an RODC

Preparation

To prestage an RODC account, the computer name must not be in use in the domain. Therefore, you first
need to remove LON-SVR1 from the domain by performing the following steps:
1. On LON-SVR1, in Server Manager, on the left side, click Local Server.
2. In the Properties for LON-SVR1 section, click the domain Adatum.com.
3. In the System Properties dialog box, click Change.
4. In the Computer Name/Domain Changes dialog box, in the Member of section, select Workgroup,
type MUNICH, and then click OK.
5. In the Computer Name/Domain Changes dialog box, click OK.
6. In the Computer Name/Domain Changes dialog box, you will see the following message: “Welcome
to the MUNICH workgroup.” Click OK.
7. In the Computer Name/Domain Changes dialog box, you will see the following message: “You must
restart your computer to apply these changes.” Click OK.
8. In the System Properties dialog box, click Close.
9. In the Microsoft Windows dialog box, click Restart Now.
10. Sign in as:
o User name: Administrator
o Password: Pa55w.rd
11. Switch to LON-DC1. In Server Manager, click Tools, and then click Active Directory Users and
Computers.
12. In the navigation pane, expand Adatum.com, click to select Adatum Servers, right-click LON-SVR1,
and then click Delete.
13. In the Active Directory Domain Services dialog box, confirm the deletion by clicking Yes.
14. In the Confirm Subtree Deletion dialog box, click Yes.

Stage a delegated installation of an RODC

1. On LON-DC1, in Server Manager, click Tools, and then click Active Directory Sites and Services.
2. In Active Directory Sites and Services, in the navigation pane, click Sites. From the Action menu,
click New Site.
3. In the New Object – Site dialog box, in the Name field, type Munich, select the DEFAULTIPSITELINK
site link object, and then click OK.
4. In the Active Directory Domain Services dialog box, click OK.
5. Switch to Server Manager, click Tools, and then click Active Directory Administrative Center.
6. In Active Directory Administrative Center, in the navigation pane, click Adatum (local), and then in
the details pane, double-click the Domain Controllers OU.
7. In the Tasks pane, in the Domain Controllers section, click Pre-create a Read-only domain
controller account.
8. In the Active Directory Domain Services Installation Wizard, on the Welcome to the Active
Directory Domain Services Installation Wizard page, click Next.
9. On the Network Credentials page, click Next.
10. On the Specify the Computer Name page, type the computer name LON-SVR1, and then click Next.
11. On the Select a Site page, click Munich, and then click Next.
12. On the Additional Domain Controller Options page, accept the default selections of DNS Server
and Global Catalog, and then click Next.
13. On the Delegation of RODC Installation and Administration page, click Set.
14. In the Select User or Group dialog box, in the Enter the object name to select field, type Nestor,
and then click Check Names.
15. Verify that Nestor Fiore is resolved, and then click OK.
16. On the Delegation of RODC Installation and Administration page, click Next.
17. On the Summary page, review your selections, and then click Next.
18. On the Completing the Active Directory Domain Services Installation Wizard page, click Finish.
 

Task 2: Run the Active Directory Domain Services Installation Wizard on an RODC to
complete the deployment process
1. Switch to LON-SVR1. From Server Manager, click Manage, and then click Add Roles and Features.
2. In the Add Roles and Features Wizard, on the Before You Begin page, click Next.
3. On the Select installation type page, accept the default of Role-based or feature-based
installation, and then click Next.
4. On the Select destination server page, accept the default with LON-SVR1 being selected, and then
click Next.
5. On the Select server roles page, in the Roles list, select Active Directory Domain Services.
6. In the Add Roles and Features Wizard, accept to install the features and management tools, click
Add Features, and then click Next.
7. On the Select features page, click Next.
8. On the Active Directory Domain Services page, click Next.
9. On the Confirm installation selections page, click Install.
10. Wait until the role installs. You can click Close at any time, but monitor the Notification icon in Server
Manager.
11. When the installation of the new role is finished, click the Notification icon for notifications.
12. In the Post-deployment Configuration message box, click Promote this server to a domain
controller.
13. In the Active Directory Domain Services Configuration Wizard, on the Deployment
Configuration page, leave the default to Add a domain controller to an existing domain.
14. In the Supply the credentials to perform this operation section, click Change.
15. In the Windows Security dialog box, enter the following credentials and then click OK:
o User name: Adatum\Nestor
o Password: Pa55w.rd
16. Under Specify the domain information for this operation, click Select, then select the domain
Adatum.com, click OK, and then click Next.
You will receive a notification that an RODC account that matches the name of the server exists in the
directory.
17. On the Domain Controller Options page, accept the default to Use existing RODC account, in the
Password and Confirm password fields, type Pa55w.rd, and then click Next.
18. On the Additional Options page, accept the defaults, and then click Next.
19. On the Paths page, accept the defaults, and then click Next.
20. On the Review Options page, review your options, and then click Next.
21. After the prerequisites check has been performed, click Install.
Note: The computer will configure AD DS and restart, but you can proceed to the next task.


Task 3: Configure the domain-wide password replication policy
1. Switch to LON-DC1. In Server Manager, click Tools, and then click Active Directory Administrative
Center.
2. In Active Directory Administrative Center, in the navigation pane, click Adatum (local).
3. In the details pane, double-click IT.
4. Locate the IT group, right-click the group, and then click Add to another group.
5. In the Select Groups dialog box, in the Enter the object names to select text box, type denied, and
then click Check Names.
6. Verify that the name of the group is expanded to Denied RODC Password Replication Group, and
then click OK.
Note: The members of the IT group have elevated permissions, so storing their password on
an RODC would be a security risk. Therefore, you add the IT group to the global Deny List, which
applies to every RODC in the domain.
7. Close the Active Directory Administrative Center.


Task 4: Create a group to manage password replication to the branch office RODC
1. Switch to Server Manager, click Tools, and then click Active Directory Users and Computers.
2. In the navigation pane, expand Adatum.com, and then click Users.
3. On the Action menu, click New, and then click Group.
4. In the New Object – Group dialog box, type the group name Munich Allowed RODC Password
Replication Group, click OK, and then double-click the Munich Allowed RODC Password
Replication Group.
5. On the Members tab, click Add.
6. In the Select Users, Contacts, Computers, Services Accounts, or Groups dialog box, in the Enter
the object names to select text box, type Ana, and then click Check Names.
7. In the Multiple Names Found dialog box, select Ana Cantrell, and then click OK.
8. In the Select Users, Contacts, Computers, Service Accounts or Groups dialog box, click OK, and
then in the Munich Allowed RODC Password Replication Group Properties dialog box, click OK.
9. Close Active Directory Users and Computers.
10. In Active Directory Administrative Center, from the Domain Controllers OU, view the properties
for LON-SVR1.
11. In the Extensions section, on the Password Replication Policy tab, click Add.
12. In the Add Groups, Users and Computers dialog box, select Allow passwords for the account to
replicate to this RODC, and then click OK.
13. In the Select Users, Computers, Service Accounts, or Groups dialog box, in the Enter the object
names to select text box, type Munich, click Check Names, and then click OK.
14. In the LON-SVR1 dialog box, click OK to close the dialog box.


Task 5: Evaluate the resultant password replication policy
1. In Active Directory Administrative Center, in the Tasks pane, in the LON-SVR1 section, click
Properties.
2. In the properties of LON-SVR1, in the Extensions section, on the Password Replication Policy tab,
click Advanced.
Note: Note that this dialog box shows all accounts with passwords that are stored in the
RODC.
3. Select Accounts that have been authenticated to this Read-only Domain Controller, and then
note that this only shows accounts that have the permissions and already have been authenticated by
this RODC.
4. Click the Resultant Policy tab, and then add Ana Cantrell. Notice that Ana Cantrell has a resultant
policy of Allow.
5. Close all open dialog boxes.
Results: After this exercise, you should have deployed and configured an RODC.
Exercise 3: Creating and associating a group MSA


Task 1: Create and associate an MSA
1. On LON-DC1, in Server Manager, click Tools, and then click Active Directory Module for Windows
PowerShell.
2. At the Windows PowerShell command prompt, type the following command, and then press Enter:
Add-KdsRootKey –EffectiveTime ((get-date).addhours(-10))
3. At the Windows PowerShell command prompt, type the following command, and then press Enter:
New-ADServiceAccount –Name Webservice –DNSHostName LON-DC1 –
PrincipalsAllowedToRetrieveManagedPassword LON-DC1$
4. At the Windows PowerShell command prompt, type the following command, and then press Enter:
Add-ADComputerServiceAccount –identity LON-DC1 –ServiceAccount Webservice
5. At the Windows PowerShell command prompt, type the following command, and then press Enter:
Get-ADServiceAccount -Filter *
6. Note the output of the command, and then ensure the newly-created account is listed.
7. Minimize the Windows PowerShell command window.


Task 2: Install a group MSA
1. On LON-DC1, at the Windows PowerShell command prompt, type the following command, and then
press Enter:
Install-ADServiceAccount –Identity Webservice
2. In Server Manager, click the Tools menu, and then click Internet Information Services (IIS)
Manager.
3. Expand LON-DC1 (Adatum\Administrator), and then click Application Pools.
4. In the details pane, right-click the DefaultAppPool, and then click Advanced Settings.
5. In the Advanced Settings dialog box, in the Process Model section, click Identity, and then click the
ellipsis (…).
6. In the Application Pool Identity dialog box, click Custom Account, and then click Set.
7. In the Set Credentials dialog box, type Adatum\Webservice$ in the User name field, and then click
OK three times.
8. In the Actions pane, click Stop to stop the application pool.
9. Click Start to start the application pool.
10. Close Internet Information Services (IIS) Manager.
Results: After completing this exercise, you should have configured an MSA.

Task 3: Prepare for the next module
When you finish the lab, revert the virtual machines to their initial state. To do this, perform the following
steps:
1. On the host computer, start Hyper-V Manager.
2. In the Virtual Machines list, right-click 20742B-LON-DC1, and then click Revert.
3. In the Revert Virtual Machine dialog box, click Revert.
4. Repeat steps two and three for 20742B-LON-SVR1.

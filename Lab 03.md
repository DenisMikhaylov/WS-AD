
Lab: Implementing AD DS sites and replication

Scenario
A. Datum Corporation has deployed a single AD DS domain, with all the domain controllers located in the
London datacenter. As the company has grown and added branch offices with large numbers of users, it
has become apparent that the current AD DS environment does not meet the company’s requirements.
Users in some branch offices report that it can take a long time for them to sign in to their computers.
Access to network resources such as the company’s servers, which are running Microsoft Exchange Server
2016 and Microsoft SharePoint Server 2016, can be slow, and they sporadically fail.

As one of the senior network administrators, you are responsible for planning and implementing an AD DS
infrastructure that will help address the organization’s business requirements. You are responsible for
configuring AD DS sites and replication to optimize the user experience and network utilization within the
organization.
Objectives

After completing this lab, you will be able to:
 Modify the default site that was created in AD DS.
 Create and configure additional sites and subnets.
 Configure AD DS replication.
 Monitor and troubleshoot AD DS replication.

Exercise 1: Modifying the default site
Scenario
A. Datum has decided to implement additional AD DS sites to optimize the network utilization for AD DS
network traffic. Your first step in implementing the new environment is to install a new domain controller
for the Toronto site. You then will reconfigure the default site and assign appropriate IP address subnets to
the site.
Finally, your task is to change the name of the default site to LondonHQ and associate it with the
172.16.0.0/24 IP subnet, which is the subnet range for the London head office.
The main tasks for this exercise are as follows:
1. Install the Toronto domain controller.
2. Rename the default site.
3. Configure IP subnets that are associated with the default site.

 Task 1: Install the Toronto domain controller
0. Log on to LON-SVR3 and change IP to 172.16.1.10
1. On LON-SVR3, click Start, and then click Server Manager.
2. In Server Manager, click Manage, and then from the drop-down list, click Add Roles and Features.
3. On the Before you begin page, click Next.
4. On the Select installation type page, confirm that Role-based or feature-based installation is
selected, and then click Next.
5. On the Select destination server page, ensure that Select a server from the server pool is selected
and that LON-SVR3.adatum.com is highlighted, and then click Next.
6. On the Select server roles page, select the Active Directory Domain Services check box.
7. On the Add features that are required for Active Directory Domain Services? page, click Add
Features, and then click Next.
8. On the Select features page, click Next.
9. On the Active Directory Domain Services page, click Next.
10. On the Confirm installation selections page, click Install.
Note: This might take a few minutes to complete.
11. When the AD DS binaries have installed, do not click Close, but click the blue Promote this server to a
domain controller link.
12. In the Deployment Configuration window, click Add a domain controller to an existing domain,
and then click Next.
13. In the Domain Controller Options window, ensure that both the Domain Name system (DNS)
server and Global Catalog (GC) check boxes are selected.
14. Confirm that Site name: is set to Default-First-Site-Name, and then under Type the Directory
Services Restore Mode (DSRM) password, type Pa55w.rd in both the Password and Confirm
password boxes. Click Next.
15. On the DNS Options page, click Next.
16. In the Additional Options page, click Next.
17. In the Paths window, click Next.
18. In the Review Options window, click Next.
19. In the Prerequisites Check window, click Install. The server will restart automatically.
20. After LON-SVR3 restarts, sign in as Adatum\Administrator with the password Pa55w.rd.

Task 2: Rename the default site
1. If necessary, on LON-DC1, open the Server Manager console.
2. In Server Manager, click Tools, and then click Active Directory Sites and Services.
3. In Active Directory Sites and Services, in the navigation pane, expand Sites.
4. Right-click Default-First-Site-Name, and then click Rename.
5. Type LondonHQ, and then press Enter.
6. Expand LondonHQ, expand the Servers folder, and then verify that both LON-DC1 and LON-SVR3
belong to the LondonHQ site.

Task 3: Configure IP subnets that are associated with the default site
1. If necessary, on LON-DC1, open the Server Manager console, and then open Active Directory Site
and Services.
2. In the Active Directory Sites and Services console, in the navigation pane, expand Sites, and then
click the Subnets folder.
3. Right-click Subnets, and then click New Subnet.
4. In the New Object – Subnet dialog box, under Prefix, type 172.16.0.0/24.
5. Under Select a site object for this prefix, click LondonHQ, and then click OK.
Results: After completing this exercise, you should have successfully reconfigured the default site and
assigned IP address subnets to the site.

Exercise 2: Creating additional sites and subnets
Task 1: Create the AD DS sites for Toronto
1. If necessary, on LON-DC1, open the Server Manager console, click Tools, and then click Active
Directory Sites and Services.
2. In the Active Directory Sites and Services console, in the navigation pane, right-click Sites, and then
click New Site.
3. In the New Object – Site dialog box, in the Name text box, type Toronto.
4. Under Select a site link object for this site, select DEFAULTIPSITELINK, and then click OK.
5. In the Active Directory Domain Services dialog box, click OK. The Toronto site displays in the
navigation pane.
6. In the Active Directory Sites and Services console, in the navigation pane, right-click Sites, and then
click New Site.
7. In the New Object – Site dialog box, in the Name text box, type TestSite.
8. Under Select a site link object for this site, select DEFAULTIPSITELINK, and then click OK. The test
site displays in the navigation pane.

Task 2: Create IP subnets that are associated with the Toronto sites
1. If necessary, on LON-DC1, open the Server Manager console, click Tools, and then click Active
Directory Sites and Services.
2. In the Active Directory Sites and Services console, in the navigation pane, expand Sites, and then
click the Subnets folder.
3. Right-click Subnets, and then click New Subnet.
4. In the New Object – Subnet dialog box, under Prefix, type 172.16.1.0/24.
5. Under Select a site object for this prefix, click Toronto, and then click OK.
6. Right-click Subnets, and then click New Subnet.
7. In the New Object – Subnet dialog box, under Prefix, type 172.16.100.0/24.
8. Under Select a site object for this prefix, click TestSite, and then click OK.
9. In the navigation pane, click the Subnets folder. Verify in the details pane that the two subnets are
created and associated with their appropriate site.
Note: There are three subnets in total (172.16.0.0 was created in Exercise 1, Task 3,
“Configure IP subnets that are associated with the default site”).
Results: After completing this exercise, you should have successfully created two additional sites
representing the IP subnet addresses in Toronto.

Exercise 3: Configuring AD DS replication

Task 1: Configure site links between AD DS sites
1. If necessary, on LON-DC1, open the Server Manager console, click Tools, and then click Active
Directory Sites and Services.
2. In the Active Directory Sites and Services console, in the navigation pane, expand Sites, expand
Inter-Site Transports, and then click the IP folder.
3. Right-click IP, and then click New Site Link.
4. In the New Object – Site Link dialog box, in the Name text box, type TOR-TEST.
5. Under Sites not in this site link, press Ctrl on the keyboard, click Toronto, click TestSite, click Add,
and then click OK.
6. Right-click TOR-TEST, and then click Properties.
7. In the TOR-TEST Properties dialog box, click Change Schedule.
8. In the Schedule for TOR-TEST dialog box, highlight the range from Monday 9 AM to Friday 3 PM, as
follows:
o Click the Monday at 9:00AM tile, press and hold the mouse button, and then drag the cursor to
the Friday at 3:00 PM tile.
9. Click Replication Not Available, and then click OK.
10. Click OK to close TOR-TEST Properties.MCT USE ONLY. STUDENT USE PROHIBITED
L4-26 Implementing and administering AD DS sites and replication
11. Right-click DEFAULTIPSITELINK, and then click Rename.
12. Type LON-TOR, and then press Enter.
13. Right-click LON-TOR, and then click Properties.
14. Under Sites in this site link, click TestSite, and then click Remove.
15. In the Replicate Every spin box, change the value to 60 minutes, and then click OK.

Task 2: Move LON-SVR3 to the Toronto site
1. If necessary, on LON-DC1, click Tools, and then click Active Directory Sites and Services.
2. In the Active Directory Sites and Services console, in the navigation pane, expand Sites, expand
LondonHQ, and then expand the Servers folder.
3. Right-click LON-SVR3, and then click Move.
4. In the Move Server dialog box, click Toronto, and then click OK.
5. In the navigation pane, expand the Toronto site, expand Servers, and then click LON-SVR3.

Task 3: Monitor AD DS site replication
1. On LON-DC1, click Start, and then click the Windows PowerShell icon.
2. At the Windows PowerShell prompt, type the following, and then press Enter:
Repadmin /kcc
This command recalculates the inbound replication topology for the server.
3. At the Windows PowerShell command prompt, type the following command, and then press Enter:
Repadmin /showrepl
4. Verify that the last replication with LON-SVR3 was successful.
5. At the Windows PowerShell command prompt, type the following command, and then press Enter:
Repadmin /bridgeheads
This command displays the bridgehead servers for the site topology.
6. At the Windows PowerShell command prompt, type the following, and then press Enter:
Repadmin /replsummary
This command displays a summary of replication tasks. Verify that no errors appear.
7. At the Windows PowerShell command prompt, type the following, and then press Enter:
DCDiag /test:replications
8. Verify that all connectivity and replication tests pass successfully.
9. Switch to LON-SVR3, and then repeat steps 1 through 8 to view information from LON-SVR3. For step 4,
verify that the last replication with LON-DC1 was successful.
Results: After completing this exercise, you should have successfully configured site links and monitored
replication.


Exercise 4: Monitoring and troubleshooting AD DS replication

Task 1: Produce an error
1. If necessary, on LON-DC1, open Server Manager.
2. In Server Manager, click Tools, and then click Active Directory Sites and Services.
3. In the Active Directory Sites and Services console, in the navigation pane, expand Sites, expand
LondonHQ, expand the Servers folder, expand LON-DC1, and then select NTDS Settings.
4. In the details pane, right-click the LON-SVR3 connection object, and then click Replicate Now.
5. In the Replicate Now dialog box, click OK.
6. In Active Directory Sites and Services, examine all the objects you created earlier, and then on the
taskbar, click the Windows PowerShell icon.
7. At the Windows PowerShell command prompt, type the following, and then press Enter:
Get-ADReplicationUpToDatenessVectorTable –Target “adatum.com”
Note: This cmdlet will show you the last several replication events. Make a note of the date
and time of the last (top) event.
8. Go to LON-SVR3.
9. Click Start, and the click Windows PowerShell.
10. At the Windows PowerShell command prompt, type the following, and then press Enter after each
command:
```
CD \Labfiles\Mod04
.\Mod04Ex4.ps1
```
Task 2: Monitor AD DS site replication
1. If necessary, on LON-SVR3, open the Server Manager console, click Tools, and then click Active
Directory Sites and Services.
2. In the Active Directory Sites and Services console, in the navigation pane, expand Sites, expand
Toronto, expand Servers, expand LON-SVR3, and then select NTDS Settings.
3. In the details pane, right click LON-DC1, and then select Replicate Now.
4. Click OK on the Replicate Now pop-up.
5. On LON-SVR3, on the taskbar, click the Windows PowerShell icon.
6. At the Windows PowerShell command prompt, type the following, and then press Enter:
Get-ADReplicationUpToDatenessVectorTable –Target “adatum.com”
Note: This cmdlet will show you the last several replication events. Note that the last date
and time shown (Replication from LON-DC1) is not updating. This indicates that one-way
replication is not occurring.
7. At the Windows PowerShell command prompt, type the following, and then press Enter:
```
Get-AdReplicationSubnet –filter *
```
8. At the Windows PowerShell command prompt, type the following, and then press Enter:
```
Get-AdReplicationSiteLink –filter *
```
 Task 3: Troubleshoot AD DS replication
1. If necessary, on LON-SVR3, open Windows PowerShell.
2. At the Windows PowerShell command prompt, type the following, and then press Enter:
Ipconfig /all
3. Examine the results. The DNS server address should be 10.0.0.1.
4. At the Windows PowerShell command prompt, type the following, and then press Enter:
```
Get-DnsClient | Set-DnsClientServerAddress -ServerAddresses ("172.16.0.10","172.16.0.25")
```
5. Run the Ipconfig /all command again. The DNS server addresses should be 172.16.0.10 and
172.16.0.25.
6. If necessary, on LON-SVR3, open the Server Manager console, click Tools, and then click Active
Directory Sites and Services.
7. In the Active Directory Sites and Services console, in the navigation pane, expand Sites, expand
Toronto, expand Servers, expand LON-SVR3, and then select NTDS Settings.
8. In the details pane, right click LON-DC1, and then select Replicate Now.
9. In the Replication Now window, click OK.
10. In Active Directory Sites and Services, examine all objects that you created earlier. Are any missing?
11. On LON-SVR3, open File Explorer. Browse to C:\Labfiles\Mod04.
12. Right-click the Mod04EX4Fix.ps1 file, and then select Run with PowerShell. Type Y when prompted
about execution policy, and then press Enter.
13. In Active Directory Sites and Services, examine all the objects that you created earlier. Ensure that
the site link has been created in the Inter-Site Transports node, and subnets have been created in the
Subnets node.
14. On LON-DC1 and LON-SVR3, close all open windows, and then sign out of both virtual machines.
Results: After completing this exercise, you should have successfully diagnosed and resolved replication
issues.

Task 3: Prepare for the next module
When you finish the lab, revert the virtual machines to their initial state. To do this, complete the following
steps:
1. On the host computer, start Hyper-V Manager.
2. On the Virtual Machines list, right-click LON-DC1, and then click Revert.
3. In the Revert Virtual Machine dialog box, click Revert.
4. Repeat steps 2 and 3 for LON-SVR3.

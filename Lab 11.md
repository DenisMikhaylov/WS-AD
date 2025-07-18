Exercise 1: Installing and Configuring DNS

Task 1: Configure LON-SVR1 as a domain controller without installing the Domain
Name System (DNS) server role
1. On LON-SVR1, in the Server Manager console, click Add roles and features.
2. On the Before you begin page, click Next.
3. On the Select installation type page, click Next.
4. On the Select destination server page, ensure that LON-SVR1.Adatum.com is selected, and then
click Next.
5. On the Select server roles page, select Active Directory Domain Services.
6. When Add Roles and Features Wizard appears, click Add Features, and then click Next.
7. On the Select features page, click Next.
8. On the Active Directory Domain Services page, click Next.
9. On the Confirm installation selections page, click Install.
10. On the Installation progress page, when the Installation succeeded message appears, click Close.
11. In the Server Manager console, on the navigation page, click AD DS.
12. On the title bar where Configuration required for Active Directory Domain Services at
LON-SVR1 is visible, click More.
13. On the All Server Task Details and Notifications page, click Promote this server to a domain
controller.
14. In the Active Directory Domain Services Configuration Wizard, on the Deployment Configuration
page, ensure that Add a domain controller to an existing domain is selected, and then click Next.
15. On the Domain Controller Options page, clear the Domain Name System (DNS) server check box,
and leave the Global Catalog (GC) check box selected.
16. Type Pa55w.rd in both text fields, and then click Next.
17. On the Additional Options page, click Next.
18. On the Paths page, click Next.
19. On the Review Options page, click Next.
20. On the Prerequisites Check page, click Install.
21. On the You’re about to be signed out app bar, click Close.
The LON-SVR1 server automatically restarts as part of the procedure.
22. After LON-SVR1 restarts, sign in as Adatum\Administrator with the password Pa55w.rd.
 Task 2: Review configuration settings on the existing DNS server to confirm root
hints
1. On LON-DC1, in the DNS Manager console, click and then right-click LON-DC1, and then click
Properties.
2. In the LON-DC1 Properties dialog box, click the Root hints tab. Ensure that root hints servers
display.
3. Click the Forwarders tab. Ensure that the list displays no entries, and that the Use root hints if no
forwarders are available option is selected.
4. Click Cancel.
5. Close the DNS Manager console.
6. In the taskbar, click the Windows PowerShell icon.
7. In Windows PowerShell, type the following cmdlets, press Enter after each, and observe the output
returned:
Get-DnsServerRootHint
Get-DnsServerForwarder
Note that both cmdlets are the respective Windows PowerShell equivalents of the DNS Console
actions performed in steps 2 and 3 above.
 Task 3: Add the DNS server role for the branch office on the domain controller
1. On LON-SVR1, in the Server Manager console, click Add roles and features.
2. On the Before you begin page, click Next.
3. On the Select installation type page, click Next.
4. On the Select destination server page, ensure that LON-SVR1.Adatum.com is selected, and then
click Next.
5. On the Select server roles page, select DNS Server.
6. When the Add Roles and Features Wizard appears, click Add Features, and then click Next.
7. On the Select Features page, click Next.
8. On the DNS Server page, click Next.
9. On the Confirm installation selections page, click Install.
10. On the Installation progress page, when the “Installation succeeded” message appears, click Close.
 Task 4: Verify replication of the Adatum.com Active Directory–integrated zone
1. On LON-SVR1, in the Server Manager console, click Tools.
2. On the list of tools, click DNS.
3. In the DNS Manager console, expand LON-SVR1, and then expand Forward Lookup Zones.
This container is probably empty.
4. Switch back to Server Manager, click Tools, and then click Active Directory Sites and Services.
5. In the Active Directory Sites and Services console, expand Sites, expand Default-First-Site-Name,
expand Servers, expand LON-DC1, and then click NTDS Settings. 
6. In the right pane, right-click the LON-SVR1 replication connection, and select Replicate Now.
Note: If you receive an error message, proceed to the next step, and then retry this step
after three to four minutes. If this retry fails, wait a few more minutes, and then try again.
7. In the navigation pane, expand LON-SVR1, and then click NTDS Settings.
8. In the right pane, right-click the LON-DC1 replication connection, click Replicate Now, and then
click OK.
9. Switch back to the DNS Manager console, right-click Forward Lookup Zones, and then click
Refresh.
10. Ensure that both the _msdcs.Adatum.com and Adatum.com containers display.
11. Close DNS Manager.
 Task 5: Create and configure Contoso.com zone on LON-DC1
1. On the LON-DC1 virtual machine, in the Server Manager console, click Tools, and then click DNS.
2. Expand LON-DC1, right-click Forward Lookup Zones, and then select New Zone.
3. In the New Zone Wizard, on the Welcome to the New Zone Wizard page, click Next.
4. On the Zone Type page, clear the Store the zone in Active Directory check box, and then click
Next.
5. On the Zone Name page, type Contoso.com, and then click Next.
6. On the Zone File page, click Next.
7. On the Dynamic Update page, click Next.
8. On the Completing the New Zone Wizard page, click Finish.
9. Expand Forward Lookup Zones, and then select and right-click contoso.com zone, and click New
Host (A or AAAA).
10. In the New Host window, in the Name textbox type www.
11. In the IP address box, type 172.16.0.100.
12. Click Add Host.
13. Click OK, and then click Done.
14. Leave the DNS Manager console open.
 Task 6: Use Windows PowerShell commands to test non-local resolution
1. On LON-SVR1, on the taskbar, click the Windows PowerShell icon.
2. In Windows PowerShell, type the following cmdlet, and then press Enter:
Get-DnsClient
3. Note the entries labeled Ethernet in the InterfaceAlias column. In the Interface Index column, note
the Interface Index number that is in the same row as Ethernet and IPv4. Write this number here:
4. In Windows PowerShell, type the following cmdlet, where X is the specific Interface Index number you
wrote down in the last step, and then press Enter:
Set-DnsClientServerAddress –InterfaceIndex X –ServerAddress 127.0.0.1
5. In Windows PowerShell, type the following, and then press Enter:
Resolve-DNSName www.contoso.com
You should receive an error message in red text. This is expected.
6. In Windows PowerShell, type the following, and then press Enter:
nslookup
7. At the nslookup > prompt, type the following, and then press Enter:
www.contoso.com
You should see the following reply:
“Server: localhost
Address: 127.0.0.1
DNS request timed out.
timeout was 2 seconds.
DNS request timed out.
timeout was 2 seconds.
*** Request to localhost timed-out.”
8. Type the following, and then press Enter:
Exit
9. Leave the Windows PowerShell window open.
 Task 7: Configure Internet name resolution to forward to the head office
1. At the Windows PowerShell prompt, type the following cmdlet, and then press Enter:
Set-DnsServerForwarder –IPAddress '172.16.0.10' –PassThru
2. At the Windows PowerShell prompt, type the following two cmdlets, and press Enter after each one:
Stop-Service DNS
Start-Service DNS
 Task 8: Use Windows PowerShell to confirm name resolution
1. Sign in to LON-SVR1 as Adatum\Administrator with the password Pa55w.rd.
2. On LON-SVR1, switch to a Windows PowerShell window.
3. Type the following cmdlet, and then press Enter:
nslookup www.contoso.com
Ensure that you receive an IP address for this host as a non-authoritative answer.
4. Close Windows PowerS

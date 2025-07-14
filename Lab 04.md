Lab: Domain and trust management in AD DS

Scenario
A. Datum has deployed a single AD DS domain with all the domain controllers located in its London
datacenter. As the company has grown and added branch offices with a large numbers of users, it has
become increasingly apparent that the current AD DS environment does not meet company requirements.
The network team is concerned about the amount of AD DS–related network traffic that is crossing WAN
links, which are becoming highly utilized.
The company has also become increasingly integrated with partner organizations, some of which need
access to shared resources and applications that are located on the A. Datum internal network. The Security
department at A. Datum wants to ensure that access for these external users is as secure as possible.
As one of the senior network administrators at A. Datum, you are responsible for implementing an AD DS
infrastructure that meets company requirements. You are responsible for planning an AD DS domain and
forest deployment that provides optimal services for internal and external users while addressing the
security requirements at A. Datum.
Objectives
After completing this lab, you will be able to:
Implement child domains in AD DS.

Exercise 1: Implementing child domains in AD DS

Task 1: Install a domain controller in a child domain
1. On LON-SVR2, click Start, and then click Server Manager. In Server Manager, click Manage, and then
in the drop-down list, click Add Roles and Features.
2. On the Before you begin page, click Next.
3. On the Select installation type page, confirm that the Role-based or feature-based installation
option is selected, and then click Next.
4. On the Select destination server page, ensure that the Select a server from the server pool option
is selected and that LON-SVR2.adatum.com is highlighted, and then click Next.
5. On the Select server roles page, click Active Directory Domain Services.
6. On the Add features that are required for Active Directory Domain Services? page, click Add
Features.
7. On the Select server roles page, click Next.
8. On the Select features page, click Next.
9. On the Active Directory Domain Services page, click Next.
10. On the Confirm installation selections page, click Install. This might take a few minutes to complete.
11. When the Active Directory Domain Services (AD DS) binaries have installed, click the blue Promote
this server to a domain controller link.
12. In the Deployment Configuration window, click Add a new domain to an existing forest.
13. Verify that Select domain type is set to Child Domain and that Parent domain name is set to
Adatum.com.
14. In the New domain name text box, type na.
15. Confirm that Supply the credentials to perform this operation is set to ADATUM\Administrator
(Current user), and then click Next.
Note: If the credentials are not set to Adatum\Administrator, use the Change button to
enter the credentials Adatum\Administrator with the password Pa55w.rd.
16. In the Domain Controller Options window, ensure that Domain functional level is set to Windows
Server 2022.
17. Ensure that both the Domain Name system (DNS) server and Global Catalog (GC) check boxes are
selected.
18. Confirm that Site name: is set to Default-First-Site-Name.
19. Under Type the Directory Services Restore Mode (DSRM) password, type Pa55w.rd in both text
boxes, and then click Next.
20. On the DNS Options page, click Next.
21. On the Additional Options page, click Next.
22. On the Paths page, click Next.
23. On the Review Options page, click Next.
24. On the Prerequisites Check page, confirm that there are no issues, and then click Install.
Note: If you receive a “Windows Server 2022 domain controllers have a default for the
security setting named ‘Allow cryptography algorithms compatible with Windows NT 4.0’”
warning, you may safely ignore it.
After the configuration completes, the server restarts automatically.

Task 2: Verify the default trust configuration
1. Sign in to LON-SVR2 as NA\Administrator with the password Pa55w.rd.
2. Click Start, click Server Manager, and then in Server Manager, click Local Server.
3. Verify that Windows Firewall shows Domain: Off. If it does not, perform the following steps:
a. Click the underlined blue text next to Windows Firewall. In the Windows Firewall window, click
Turn Windows Firewall on or off.
b. Under each section, select Turn off Windows Firewall (not recommended), and then click OK.
Ignore any warning prompts that appear regarding Windows Firewall.
c. In Server Manager, click the Refresh "Local Server" icon, indicated by double arrows.
d. After the refresh completes, verify that Windows Firewall shows Public: Off.
4. In Server Manager, on the Tools menu, click Active Directory Domains and Trusts.
5. In the Active Directory Domains and Trusts console, expand Adatum.com, right-click
na.adatum.com, and then click Properties.
6. In the na.adatum.com Properties dialog box, click the Trusts tab, in the Domains trusted by this
domain (outgoing trusts) text box, click Adatum.com, and then click Properties.
7. In the Adatum.com Properties dialog box, click Validate, and then click Yes, validate the incoming
trust.
8. In the User name text box, type administrator, in the Password text box, type Pa55w.rd, and then
click OK.
9. When the “The trust has been validated. It is in place and active” message appears, click OK.
Note: If you receive a message that the trust cannot be validated or that the secure channel
verification has failed, ensure that you have completed step 3, and then wait for at least 10–15
minutes before trying again.
10. Click OK twice to close the Adatum.com Properties dialog box.
Results: After completing this exercise, you should have successfully implemented child domains in AD DS.
 Task 3: Prepare for the next module
When you finish the lab, revert the virtual machines to their initial state. To do this, complete the following
steps:
1. On the host computer, start Hyper-V Manager.
2. In the Virtual Machines list, right-click LON-DC1, and then click Revert.
3. In the Revert Virtual Machine dialog box, click Revert.
4. Repeat steps 2 and 3 for LON-SVR2

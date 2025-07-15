Lab: Deploying and configuring a two-tier CA hierarchy

Scenario

A. Datum has expanded, therefore, its security requirements also have increased. The Security department
is particularly interested in enabling secure access to critical websites and in providing additional security
for some features. To address these and other security requirements, A. Datum has decided to implement a
PKI by using the AD CS role in Windows Server 2016. As a senior network administrator at A. Datum, you are
responsible for implementing the AD CS deployment.
Objectives

After completing this lab, you will be able to:
Deploy an offline root CA.
Deploy an enterprise subordinate CA.

Lab Setup
Estimated Time: 60 minutes
Virtual machines: LON-DC1, LON-SVR1, and LON-SVR4
User name: Adatum\Administrator
Password: Pa55w.rd

Exercise 1: Deploying an offline root CA

Task 1: Create file and printer sharing exceptions
1. Sign in to LON-SVR4 as Administrator with the password Pa55w.rd.
2. Click Start, and then click Control Panel.
3. In the Control Panel window, click View network status and tasks.
4. In the Network and Sharing Center window, click Change advanced sharing settings.
5. Under Guest or Public (current profile), select the Turn on file and printer sharing option, and
then click Save changes.
6. Switch to LON-SVR1.
7. Click Start, and then click Control Panel.
8. In the Control Panel window, click View network status and tasks.
9. In the Network and Sharing Center window, click Change advanced sharing settings.
10. Under Domain (current profile), select the Turn on file and printer sharing option, and then click
Save changes.


Task 2: Install and configure Active Directory Certificate Services (AD CS) on LON-SVR4
1. Switch to LON-SVR4.
2. Click Start, and then click Server Manager.
3. In Server Manager, click Add roles and features.
4. On the Before you begin page, click Next.
5. On the Select installation type page, click Next.
6. On the Select destination server page, click Next.
7. On the Select server roles page, select Active Directory Certificate Services. When the Add Roles
and Features Wizard window displays, click Add Features, and then click Next.
8. On the Select features page, click Next.
9. On the Active Directory Certificate Services page, click Next.
10. On the Select role services page, ensure that Certification Authority is selected, and then click Next.
11. On the Confirm installation selections page, click Install.
12. On the Installation progress page, after installation completes successfully, click the Configure
Active Directory Certificate Services on the destination server text.
13. In the AD CS Configuration Wizard, on the Credentials page, click Next.
14. On the Role Services page, select Certification Authority, and then click Next.
15. On the Setup Type page, ensure that Standalone CA is selected, and then click Next.
16. On the CA Type page, ensure that Root CA is selected, and then click Next.
17. On the Private Key page, ensure that Create a new private key is selected, and then click Next.
18. On the Cryptography for CA page, keep the default selections for Select a cryptographic provider
and Select the hash algorithm for signing certificates issued by this CA, but set the Key length to
4096, and then click Next.
19. On the CA Name page, in the Common name for this CA text box, type AdatumRootCA, and then
click Next.
20. On the Validity Period page, click Next.
21. On the CA Database page, click Next.
22. On the Confirmation page, click Configure.
23. On the Results page, click Close.
24. On the Installation progress page, click Close.
25. On LON-SVR4, in Server Manager, click Tools, and then click Certification Authority.
26. In the certsrv – [Certification Authority (Local)] console, right-click AdatumRootCA, and then click
Properties.
27. In the AdatumRootCA Properties dialog box, click the Extensions tab.
28. In the Select extension drop-down list, click CRL Distribution Point (CDP), and then click Add.
29. In the Location text box, type http://lon-svr1.adatum.com/CertData/.
30. In the Variable drop-down list, click <CaName>, and then click Insert.
31. In the Variable drop-down list, click <CRLNameSuffix>, and then click Insert.
32. In the Variable drop-down list, click <DeltaCRLAllowed>, and then click Insert.
33. In the Location text box, position the cursor at the end of the URL, type .crl, and then click OK.
34. Select the following options, and then click Apply:
o Include in the CDP extension of issued certificates
o Include in CRLs. Clients use this to find Delta CRL locations
35. In the Certification Authority pop-up window, click No.
36. In the Select extension drop-down list, click Authority Information Access (AIA), and then
click Add.
37. In the Location text box, type http://lon-svr1.adatum.com/CertData/.
38. In the Variable drop-down list, click <ServerDNSName>, and then click Insert.
39. In the Location text box, type an underscore (_), in the Variable drop-down list, click <CaName>, and
then click Insert. Position the cursor at the end of the URL.
40. In the Variable drop-down list, click <CertificateName>, and then click Insert.
41. In the Location text box, position the cursor at the end of the URL, type .crt, and then click OK.
42. Select the Include in the AIA extension of issued certificates check box, and then click OK.
43. Click Yes to restart the Certification Authority service.
44. In the Certification Authority console, expand AdatumRootCA, right-click Revoked Certificates,
point to All Tasks, and then click Publish.
45. In the Publish CRL window, click OK.
46. Right-click AdatumRootCA, and then click Properties.
47. In the AdatumRootCA Properties dialog box, click View Certificate.
48. In the Certificate dialog box, click the Details tab, and then click Copy to File.
49. In the Certificate Export Wizard, on the Welcome page, click Next.
50. On the Export File Format page, select DER encoded binary X.509 (.CER), and then click Next.
51. On the File to Export page, click Browse, in the File name text box, type \\lon-svr1\C$, and then
press Enter.
52. In the File name text box, type RootCA, click Save, and then click Next.
53. Click Finish, and then click OK three times.
54. Open a File Explorer window, and then browse to C:\Windows\System32\CertSrv\CertEnroll.
55. In the Cert Enroll folder, select both files, right-click the highlighted files, and then click Copy.
56. In the File Explorer address bar, type \\lon-svr1\C$, and then press Enter.
57. Right-click the empty space, and then click Paste.
58. Close File Explorer.
 Task 3: Create a Domain Name System (DNS) record for an offline root CA
1. On LON-DC1, in Server Manager, click Tools, and then click DNS.
2. In the DNS Manager console, expand LON-DC1, expand Forward Lookup Zones, click Adatum.com,
right-click Adatum.com, and then click New Host (A or AAAA).
3. In the New Host window, in the Name text box, type LON-SVR4.
4. In the IP address window, type 172.16.0.40, click Add Host, click OK, and then click Done.
5. Close DNS Manager.
Results: After completing this exercise, you should have successfully installed and configured the
standalone root certification authority (CA) role on the LON-SVR4 server. Additionally, you should have
created an appropriate DNS record in Active Directory Domain Services (AD DS) so that other servers can
connect to LON-SVR4.


Exercise 2: Deploying an enterprise subordinate CA


Task 1: Install and configure AD CS on LON-SVR1
1. On LON-SVR1, click Start, click Server Manager, and then click Add roles and features.
2. On the Before you begin page, click Next.
3. On the Select installation type page, click Next.
4. On the Select destination server page, click Next.
5. On the Select server roles page, select Active Directory Certificate Services.
6. When the Add Roles and Features Wizard displays, click Add Features, and then click Next.
7. On the Select features page, click Next.
8. On the Active Directory Certificate Services page, click Next.
9. On the Select role services page, ensure that Certification Authority is selected already, and then
select Certification Authority Web Enrollment.
10. When the Add Roles and Features Wizard displays, click Add Features, and then click Next.
11. On the Confirm installation selections page, click Install.
12. On the Installation progress page, after installation is successful, click the Configure Active
Directory Certificate Services on the destination server text.
13. In the AD CS Configuration wizard, on the Credentials page, click Next.
14. On the Role Services page, select both Certification Authority and Certification Authority Web
Enrollment, and then click Next.
15. On the Setup Type page, select Enterprise CA, and then click Next.
16. On the CA Type page, click Subordinate CA, and then click Next.
17. On the Private Key page, ensure that Create a new private key is selected, and then click Next.
18. On the Cryptography for CA page, keep the default selections, and then click Next.
19. On the CA Name page, in the Common name for this CA text box, type Adatum-IssuingCA, and
then click Next.
20. On the Certificate Request page, ensure that Save a certificate request to file on the target
machine is selected, and then click Next.
21. On the CA Database page, click Next.
22. On the Confirmation page, click Configure.
23. On the Results page, ignore the warning messages, and then click Close.
24. On the Installation progress page, click Close.


Task 2: Install a subordinate CA certificate

1. On LON-SVR1, open a File Explorer window, and then browse to Local Disk (C:).
2. Right-click RootCA.cer, and then click Install Certificate.
3. In the Certificate Import wizard, click Local Machine, and then click Next.
4. On the Certificate Store page, click Place all certificates in the following store, and then click
Browse.
5. Select Trusted Root Certification Authorities, click OK, click Next, and then click Finish.
6. When the Certificate Import wizard window appears, click OK.
7. In the File Explorer window, Select the AdatumRootCA.crl and LON-SVR4_AdatumRootCA.crt files,
right-click the files, and then click Copy.
8. Double-click inetpub.
9. Double-click wwwroot.
10. Create a new folder, and then name it CertData.
11. Paste the two copied files into that folder.
12. Switch to Local Disk (C:).
13. Right-click the LON-SVR1.Adatum.com_Adatum-LON-SVR1-CA.req file, and then click Copy.
14. In the File Explorer address bar, type \\LON-SVR4\C$, and then press Enter.
15. In the File Explorer window, right-click an empty space, and then click Paste. Make sure that the
request file copies to LON-SVR4.
16. Switch to the LON-SVR4 server.
17. In the Certificate Authority console, right-click AdatumRootCA, point to All Tasks, and then click
Submit new request.
18. In the Open Request File window, navigate to Local Disk (C:), click the
LON-SVR1.Adatum.com_Adatum- LON-SVR1-CA.req file, and then click Open.
19. In the Certification Authority console, click the Pending Requests container. Right-click Pending
Requests, and then click Refresh.
20. In the details pane, right-click the request (with ID 2), point to All Tasks, and then click Issue.
21. In the Certification Authority console, click the Issued Certificates container.
22. In the details pane, double-click the certificate, click the Details tab, and then click Copy to File.
23. In the Certificate Export wizard, on the Welcome page, click Next.
24. On the Export File Format page, click Cryptographic Message Syntax Standard – PKCS #7
Certificates (.P7B), click Include all certificates in the certification path if possible, and then click
Next.
25. On the File to Export page, click Browse.
26. In the File name text box, type SubCA, click Save, click Next, click Finish, and then click OK twice.
27. Switch to LON-SVR1.
28. In Server Manager, click Tools, and then click Certification Authority.
29. In the Certification Authority console, right-click Adatum-IssuingCA, point to All Tasks, and then
click Install CA Certificate.
30. Go to Local Disk (C:), click the SubCA.p7b file, and then click Open.
31. Wait for 15–20 seconds, and then on the toolbar, click the green icon to start the CA service.
32. Ensure that the CA successfully starts.
33. Switch to LON-SVR4.
34. Shut down the server.
Note: From this point, you can safely take the root CA offline and use just the enterprise
subordinate CA.


Task 3: Publish a root CA certificate through Group Policy

1. On LON-DC1, in Server Manager, click Tools, and then click Group Policy Management.
2. In the Group Policy Management Console, expand Forest: Adatum.com, expand Domains, expand
Adatum.com, right-click Default Domain Policy, and then click Edit.
3. In the Computer Configuration node, expand Policies, expand Windows Settings, expand Security
Settings, expand Public Key Policies, right-click Trusted Root Certification Authorities, click
Import, and then click Next.
4. On the File to Import page, click Browse.
5. In the file name text box, type \\lon-svr1\C$, and then press Enter.
6. Click file RootCA.cer, and then click Open.
7. Click Next two times, and then click Finish.
8. When the Certificate Import wizard window appears, click OK.
Note: It might take 15–20 seconds for this window to appear.
9. Close the Group Policy Management Editor and the Group Policy Management Console.
Results: After completing this exercise, you should have successfully deployed and configured an
enterprise subordinate CA. You also should have a subordinate CA certificate issued by a root CA installed
on LON-SVR1. To establish trust between the root CA and domain member clients, you will use Group
Policy to deploy a root CA certificate.

Task 4: Prepare for the next module
After you finish the lab, revert the virtual machines to their initial state. To do this, complete the following
steps:
1. On the host computer, start Hyper-V Manager.
2. In the Virtual Machines list, right-click 20742B-LON-DC1, and then click Revert.
3. In the Revert Virtual Machine dialog box, click Revert.
4. Repeat steps 2 and 3 for LON-SVR1 and LON-SVR4

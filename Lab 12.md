Lab: Implementing DHCP
Exercise 1: Implementing DHCP
 Task 1: Install the Dynamic Host Configuration Protocol (DHCP) server role
1. Sign in to LON-SVR1 as Adatum\Administrator with the password Pa55w.rd.
2. In Server Manager, click Add roles and features.
3. In the Add Roles and Features Wizard, click Next.
4. On the Select installation type page, click Next.
5. On the Select destination server page, click Next.
6. On the Select server roles page, select the DHCP Server check box.
7. In the Add Roles and Features Wizard, click Add Features, and then click Next.
8. On the Select features page, click Next.
9. On the DHCP Server page, click Next.
10. On the Confirm installation selections page, click Install.
11. On the Installation progress page, wait until the “Installation succeeded on
LON-SVR1.Adatum.com” message appears, and then click Close.
 Task 2: Configure the DHCP scope and options
1. In the Server Manager Dashboard, click Tools, and then click DHCP.
2. In the DHCP console, expand and then right-click lon-svr1.adatum.com, and then click Authorize.
3. In the DHCP console, right-click lon-svr1.adatum.com, and then click Refresh.
Notice that the icons next to IPv4 IPv6 changes color from red to green, which means that the DHCP
server has been authorized in Active Directory® Domain Services (AD DS).
4. In the DHCP console, in the navigation pane, click lon-svr1.adatum.com, expand and right-click
IPv4, and then click New Scope.
5. In the New Scope Wizard, click Next.
6. On the Scope Name page, in the Name box, type Branch Office, and then click Next.
7. On the IP Address Range page, complete the page using the following information, and then click
Next:
o Start IP address: 172.16.0.100
o End IP address: 172.16.0.200
o Length: 16
o Subnet mask: 255.255.0.0
8. On the Add Exclusions and Delay page, complete the page using the following information:
o Start IP address: 172.16.0.190
o End IP address: 172.16.0.200
9. Click Add, and then click Next.
10. On the Lease Duration page, click Next.
11. On the Configure DHCP Options page, click Next.
12. On the Router (Default Gateway) page, in the IP address box, type 172.16.0.1, click Add, and then
click Next.
13. On the Domain Name and DNS Servers page, click Next.
14. On the WINS Servers page, click Next.
15. On the Activate Scope page, click Next.
16. On the Completing the New Scope Wizard page, click Finish.
 Task 3: Configure the client to use DHCP, and then test the configuration
1. Sign in to lon-SRV2 as Adatum\Administrator with the password Pa55w.rd.
2. On the Start page, type Control Panel, and then press Enter.
3. In Control Panel, under Network and Internet, click View Network Status and Tasks.
4. In the Network and Sharing Center window, click Change adapter settings.
5. In the Network Connections window, right-click Ethernet, and then click Properties.
6. In the Ethernet Properties window, click Internet Protocol Version 4 (TCP/IPv4), and then click
Properties.
7. In the Internet Protocol Version 4 (TCP/IPv4) Properties dialog box, select the Obtain an IP
address automatically radio button, select the Obtain DNS server address automatically radio
button, click OK, and then click Close.
8. Right-click the Start button, and then click Command Prompt.
9. In the Command Prompt window, at the command prompt, type the following, and then press Enter:
ipconfig /renew
10. To test the configuration and verify that Lon-SRV2 has received an IP address from the DHCP scope, at
a command prompt, type the following, and then press Enter:
ipconfig /all
This command returns information such as IP address, subnet mask, and DHCP enabled status, which
should be Yes.
 Task 4: Configure a lease as a reservation
1. In the Command Prompt window, at a command prompt, type the following, and then press Enter:
ipconfig /all
2. Write down the Physical Address of Lon-SRV2 network adapter.
3. Switch to LON-SVR1.
4. In the Server Manager dashboard, click Tools, and then click DHCP.
5. In the DHCP console, expand lon-svr1.adatum.com, expand IPv4, expand Scope [172.16.0.0]
Branch Office, select and then right-click Reservations, and then click New Reservation.
6. In the New Reservation window:
o In the Reservation Name field, type Lon-SRV2.
o In the IP address field, type 172.16.0.155.
o In the MAC address field, type the physical address you wrote down in step 2.
o Click Add, and then click Close.
7. Switch to Lon-SRV2.
8. In the Command Prompt window, at a command prompt, type the following, and then press Enter:
ipconfig /release
This causes Lon-SRV2 to release any currently leased IP addresses.
9. At a command prompt, type the following, and then press Enter:
ipconfig /renew
This causes Lon-SRV2 to lease any reserved IP addresses.
10. Verify that the IP address of Lon-SRV2 is now 172.16.0.155

Implementing and managing storage
Exercise 1: Implementing FSRM
 Task 1: Create a quota template
1. On LON-DC1, in Server Manager, click Add roles and features.
2. In the Add Roles and Features Wizard, click Next.
3. Confirm that Role-based or feature-based installation is selected, and then click Next.
4. Confirm that LON-DC1.Adatum.com is selected, and then click Next.
5. On the Select server roles page, expand File and Storage Services (2 of 12 Installed), expand
File and iSCSI Services (1 of 11 Installed), and then select the File Server Resource Manager
check box.
6. In the Add Roles and Features Wizard dialog box, click Add Features.
7. Click Next twice to confirm the role service and feature selection.
8. On the Confirm Installation Selections page, click Install.
9. When the installation completes, click Close.
10. In Server Manager, click Tools, and then click File Server Resource Manager.
11. In the File Server Resource Manager console, expand Quota Management, and then click Quota
Templates.
12. Right-click Quota Templates, and then click Create Quota Template.
13. In the Create Quota Template dialog box, in the Template name text box, type 500 MB Limit -
Mail to user and log to Event Viewer.
14. In the Space Limit text box, type 500, and ensure that the unit is MB and the option for Hard quota.
Do not allow users to exceed limit is selected.
15. In the Notification thresholds section, click Add.
16. In the Add Threshold dialog box, in the Generate notifications when usage reaches (%) text box,
type 75.
17. On the E-mail Message tab, select the Send e-mail to the user who exceeded the threshold
check box.
18. Click the Event Log tab.
19. In the File Server Resource Manager dialog box, click Yes.
20. On the Event Log tab, select the Send warning to event log check box, and then click OK.
21. In the File Server Resource Manager dialog box, click Yes.
22. In the Create Quota Template window, click OK.
 Task 2: Configure a quota based on the quota template
1. In the File Server Resource Manager console, click Quotas.
2. Right-click Quotas, and then click Create Quota.
3. In the Create Quota window, in the Quota path text box, type E:\Labfiles\Mod02\Home.
4. Select the Auto apply template and create quotas on existing and new subfolders option.
5. In the Derive properties from this quota template (Recommended) drop-down list box, click
500 MB Limit - Mail to user and log to Event Viewer.
6. Click Create.
 Task 3: Test that the quota is functional
1. Switch to LON-svr2, and then sign in as Adatum\Abbi with the password Pa55w.rd.
2. On LON-svr2, on the taskbar, click the File Explorer icon.
3. In the File Explorer window, in the tree pane, click This PC.
4. Notice that drive P only has 500 megabytes (MB) available space.
 Task 4: Create a file screen
1. Switch to LON-DC1.
2. In the File Server Resource Manager console tree, expand File Screening Management, and then
click File Screens.
3. Right-click File Screens, and then click Create File Screen.
4. In the Create File Screen window, in the File screen path text box, type E:\Labfiles\Mod02\Home.
5. In the Create File Screen window, click the Derive properties from this file screen template
(recommended) drop-down list box, and then click Block Audio and Video Files.
6. Click Create.
 Task 5: Create a file group
1. On LON-DC1, right-click File Server Resource Manager (Local), and then click Configure Options.
2. In the File Server Resource Manager Options dialog box, click the File Screen Audit tab.
3. On the File Screen Audit tab, select the Record file screening activity in auditing database check
box, and then click OK.
4. In the File Server Resource Manager console tree, click File Groups.
5. Right-click File Groups, and then click Create File Group.
6. In the Create File Group Properties window, in the File group name text box, type Adatum Media
Files Group.
7. In the Files to include text box, type *.mp*, and then click Add.
8. In the Files to exclude box, type *.mpp, click Add, and then click OK.
Note: For the purposes of this course, only a sample of digital-media extensions is being
added here. To limit all digital media files, you need to add more extensions to the file group.
9. In the File Server Resource Manager console tree, click File Screen Templates.
10. In the content pane, right-click the Block Audio and Video Files template, and then click Edit
Template Properties.
11. On the Settings tab, under File groups, click to clear the Audio and Video Files check box.
12. Select the Adatum Media Files Group check box, and then click OK.
13. At the message prompt, click Yes, and then click OK.

 Task 6: Test the file screen
1. Switch to LON-svr2.
2. In the File Explorer window, in the right pane, double-click Abbi (\\LON-DC1\Home) (P:).
3. In the right pane, right-click and point to New, and then click Text Document.
4. On the ribbon, click the View tab, and then select the File name extensions check box.
5. Right-click New Text Document.txt, and then click Rename.
6. Select the whole file name, type musicfile.mp3, and then press Enter.
7. Click Yes to change the file-name extension.
8. Notice the File Access Denied dialog box that opens.
9. Click Cancel.

 Task 7: Generate an on-demand storage report
1. Switch to LON-DC1.
2. In the File Server Resource Manager console, click Storage Reports Management.
3. Right-click Storage Reports Management, and then click Generate Reports Now.
4. In the Report data section, under Select reports to generate, select the File Screening Audit
check box.
5. Click the Scope tab, and then click Add.
6. In the Browse for Folder dialog box, browse to E:\Labfiles\Mod02\Home, and then click OK.
7. Click OK to close the Storage Reports Task Properties dialog box.
8. In the Generate Storage Reports dialog box, verify that Wait for reports to be generated and
then display them is selected, and then click OK.
9. Double-click the HTML document that starts with FileScreenAudit, and then review the generated
html reports.
10. Close all open windows on LON-DC1, except Server Manager.
Results: After completing this exercise, you should have successfully configured FSRM quotas and file
screening, and generated a storage report.


Exercise 2: Implementing Data Deduplication

 Task 1: Install the Data Deduplication role service
1. On LON-DC1, in Server Manager, click Add roles and features.
2. In the Add Roles and Features Wizard, on the Before You Begin page, click Next.
3. On the Select Installation Type page, click Next.
4. On the Select Destination Server page, click Next.
5. On the Select Server Roles page, in the Roles list, expand File and Storage Services (3 of 12
installed).
6. Expand File and iSCSI Services (2 of 11 installed).
7. Select the Data Deduplication check box, and then click Next.
8. On the Select Features page, click Next.
9. On the Confirm installation selections page, click Install.
10. When installation is complete, on the Installation progress page, click Close.

 Task 2: Enable and configure Data Deduplication
1. On LON-DC1, right-click Start, and then click Run.
2. In the Run dialog box, in the Open text box, type E:\Labfiles\Mod02\CreateLabFiles.cmd, and then
click OK.
3. On the taskbar, click the File Explorer icon.
4. If necessary, click This PC.
5. Notice that Allfiles (E:) has less than 50% free space.
6. Switch to the Server Manager window.
7. In Server Manager, in the navigation pane, click File and Storage Services, and then click Disks.
8. In the Disks pane, click 1.
9. Beneath VOLUMES, click E.
10. Right-click E, and then click Configure Data Deduplication.
11. In the Allfiles (E:\) Deduplication Settings dialog box, in the Data deduplication list, click General
purpose file server.
12. In the Deduplicate files older than (in days) text box, type 0.
13. Click Set Deduplication Schedule.
14. In the LON-DC1 Deduplication Schedule dialog box, select the Enable throughput optimization
check box, and then click OK.
15. In the Allfiles (E:\) Deduplication Settings dialog box, click OK.

 Task 3: Test Data Deduplication
1. On LON-DC1, click Start, and then click Windows PowerShell.
2. In the Windows PowerShell window, type the following command, and then press Enter:
Start-DedupJob E: -Type Optimization –Memory 50
3. Type the following command, and then press Enter:
Get-DedupJob –Volume E:
4. Switch to the File Explorer window.
5. In File Explorer, expand Allfiles (E:), expand Labfiles, expand Mod02, click Data, right-click
report.xlsx, and then click Properties.
6. In the Properties window, observe the values of Size and Size on disk, and note any differences.
7. Wait for five to ten minutes to allow the deduplication job to run.
8. Switch back to the Windows PowerShell window.
9. At the Windows PowerShell command prompt, type the following command, and then press Enter:
Get-DedupStatus –Volume E: |fl
10. Type the following command, and then press Enter:
Get-DedupVolume –Volume E: |fl
11. Type the following command, and then press Enter:
Get-DedupMetaData –Volume E: |fl
12. Switch to Server Manager.
13. In Server Manager, in the navigation pane, click File and Storage Services, and then click Disks.
14. In the DISKS pane, click 1.
15. Beneath VOLUMES, click E.
16. Observe the values for Deduplication Rate and Deduplication Savings. (You might need to click
the Server Manager refresh button to update the values.)
17. Close all open windows except Server Manager

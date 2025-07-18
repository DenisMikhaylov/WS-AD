
Lab: Implementing File and Print Services

Exercise 1: Creating and Configuring a File Share

Task 1: Create the folder structure for the new share
1. On LON-SVR1, on the taskbar, click the File Explorer icon.
2. In File Explorer, in the navigation pane, expand This PC, and then click Allfiles (E:).
3. On the menu toolbar, click Home, click New folder, type Data, and then press Enter.
4. Double-click the Data folder.
5. On the menu toolbar, click Home, click New folder, type Development, and then press Enter.
6. Repeat step 5 to create a new folder named Marketing.
 Task 2: Configure file permissions on the folder structure
To restrict access to the departmental folders, you must prevent inherited file permissions from the Data
folder from being applied to each department folder. To do this, perform the following steps.
1. In File Explorer, double-click the E:\Data folder.
2. Right-click the Development folder, and then click Properties.
3. In the Development Properties dialog box, click Security, and then click Advanced.
4. In the Advanced Security Settings for Development dialog box, click Disable Inheritance.
5. In the Block Inheritance dialog box, click Convert inherited permissions into explicit permissions
on this object.
6. Remove the two permissions entries for Users (LON-SVR1\Users), and then click OK.
7. On the Security tab, click Edit.
8. In the Permissions for Development dialog box, click Add.
9. Type Development, click Check names, and then click OK.
10. In the Permissions for Development dialog box, under Allow, select Modify permission.
11. Click OK to close the Permissions for Development dialog box.
12. Click OK to close the Development Properties dialog box.
13. Repeat steps 2 through 12 for the Marketing folder, assigning Modify permissions to the Marketing
group for their folder.
 Task 3: Create the shared folder
1. In File Explorer, navigate to drive E, right-click the Data folder, and then click Properties.
2. In the Data Properties dialog box, click the Sharing tab, and then click Advanced Sharing.
3. In the Advanced Sharing dialog box, select Share this folder, and then click Permissions.
4. In the Permissions for Data dialog box, click Add.
5. Type Authenticated Users, click Check names, and then click OK.
6. In the Permissions for Data dialog box, click Authenticated Users, and then under Allow, select
Change permission.
7. Click OK to close the Permissions for Data dialog box.
8. Click OK to close the Advanced Sharing dialog box.
9. Click Close to close the Data Properties dialog box.
 Task 4: Test access to the shared folder
1. Sign in to LON-svr2 as Adatum\Administrator with the password Pa55w.rd.
Notice that Administrator is a member of the Development group.
2. On the Start screen, click Desktop.
3. On the taskbar, click the File Explorer icon.
4. In File Explorer, in the address bar, type \\LON-SVR1\Data, and then press Enter.
5. Double-click the Development folder.
Administrator should have access to the Development folder.
6. Attempt to access the Marketing folder.
File permissions on this folder prevents you from doing this.
Administrator can still see the Marketing folder, even though he does not have access to its contents.
7. Sign out of LON-svr2.
 Task 5: Enable access-based enumeration
1. Switch to LON-SVR1.
2. On the taskbar, click the Server Manager icon.
3. In Server Manager, in the navigation pane, click File and Storage Services.
4. In the File and Storage Services window, in the navigation pane, click Shares.
5. In the Shares pane, right-click Data, and then click Properties.
6. In the Data Properties dialog box, click Settings, and then select Enable access-based
enumeration.
7. Click OK to close the Data Properties dialog box.
8. Close Server Manager.
 Task 6: Test access to the share
1. Sign in to LON-svr2 as Adatum\Administrator with the password Pa55w.rd.
2. Click the Desktop tile.
3. On the taskbar, click the File Explorer icon.
4. In File Explorer, in the address bar, type \\LON-SVR1\Data, and then press Enter.
Administrator can now view only the Development folder, the folder for which he has permissions.
5. Double-click the Development folder.
Administrator should have access to the Development folder.
6. Sign out of LON-svr2.
 Task 7: Disable offline files for the share
1. Switch to LON-SVR1.
2. On the taskbar, click the File Explorer icon.
3. In File Explorer, navigate to drive E, right-click the Data folder, and then click Properties.
4. In the Data Properties dialog box, click the Sharing tab, click Advanced Sharing, and then click
Caching.
5. In the Offline Settings dialog box, click No files or programs from the shared folder are
available offline, and then click OK.
6. Click OK to close the Advanced Sharing dialog box.
7. Click Close to close the Data Properties dialog box.
Results: After completing this exercise, you will have created a new shared folder for use by multiple
departments.

Exercise 2: Configuring Shadow Copies

 Task 1: Configure shadow copies for the file share
1. On LON-SVR1, open File Explorer.
2. Navigate to drive E, right-click Allfiles (E:), and then click Configure Shadow Copies.
3. In the Shadow Copies dialog box, click drive E, and then click Enable.
4. In the Enable Shadow Copies dialog box, click Yes.
5. In the drive Shadow Copies dialog box, click Settings.
6. In the Settings dialog box, click Schedule.
This opens the drive E:\ dialog box.
7. In drive E:\ dialog box, change Schedule Task to Daily, change Start time to 12:00 AM, and then
click Advanced.
8. In the Advanced Schedule Options dialog box, select Repeat task, and then set the frequency to
every 1 hours.
9. Select Time, and then change the time value to 11:59 PM.
10. Click OK twice, and then click OK to close the Settings dialog box.
11. Leave the drive Shadow Copies dialog box open.

 Task 2: Create multiple shadow copies of a file
1. On LON-SVR1, open File Explorer.
2. Navigate to E:\Data\Development.
3. On the menu toolbar, click Home, click New item, and then click Text Document.
4. Type Report, and then press Enter.
5. Switch back to the Shadow Copies dialog box. It should be opened on the Shadow Copies tab.
6. Click Create Now.

 Task 3: Recover a deleted file from a shadow copy
1. On LON-SVR1, switch back to File Explorer.
2. Right-click Report.txt, and then click Delete.
3. In File Explorer, right-click the Development folder, and then click Properties.
4. In the Development Properties dialog box, click the Previous Versions tab.
5. Click the most recent folder version for Development, and then click Open.
6. Confirm that Report.txt is in the folder, right-click Report.txt, and then click Copy.
7. Close the File Explorer window that just opened.
8. In the other File Explorer window, right-click the Development folder, and then click Paste.
9. Close File Explorer.
10. Click OK, and then close all open windows.

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

```


Exercise 1: Working with variable types

Scenario

You first plan to practice working with different types of variables.
The main tasks for this exercise are as follows:
1. Use string variables.
2. Use DateTime variables.

Task 1: Use string variables
1. On LON-DC1, open a Windows PowerShell prompt.
2. Create folder C:\logs
3. Create a variable $logPath that contains C:\logs\.
4. For $logPath, identify the type of variable and the available properties and methods.
5. Create a variable $logFile that contains log.txt.
6. Update $logPath to include the contents of $logFile.
7. Update the path stored in $logPath to use drive D instead of drive C.
8. Leave the Windows PowerShell prompt open for the next task.

Task 2: Use DateTime variables
1. At the Windows PowerShell prompt, create a variable $today that contains today’s date.
2. For $today, identify the type of variable and the available properties and methods.
3. Use the properties of $today to create a string in the format Year-Month-Day-Hour-Minute.txt,
and store the value in $logFile.
4. Create a variable $cutOffDay that is 30 days before today.
5. Use Get-ADUser to query user accounts that have signed in since $cutOffDay. Filter by using the
LastLogonDate property.
6. Leave the Windows PowerShell prompt open for the next exercise.
Results: After completing this exercise, you should have manipulated multiple types of variables.

Exercise 2: Using arrays

Scenario

Now that you practiced using different types of variables, you want to work with arrays.
The main tasks for this exercise are as follows:
1. Use an array to update the department for users.
2. Use an arraylist.
 Task 1: Use an array to update the department for users
1. Query all Active Directory Domain Services (AD DS) users in the Marketing department and place
them in a variable named $mktgUsers. Include the Department property in the results.
2. Use $mktgUsers to identify the number of users in the Marketing department.
3. Display the first user in $mktgUsers and verify that the Department property is listed.
4. Pipe the users in $mktgUsers to Set-ADUser and update the department to Business Development.
5. View the Department attribute in $mktgUsers to see if it has been updated.
6. Query all AD DS users in the Marketing department to verify that there are none.
7. Query all AD DS users in the Business Development department and verify that it matches the
previous count from the Marketing department.
8. Leave the Windows PowerShell prompt open for the next task.

Task 2: Use an arraylist
1. Create an arraylist named $computers with the values LON-SRV1,LON-SRV2, and LON-DC1.
2. Verify that $computers does not have a fixed size.
3. Add LON-DC2 to $computers.
4. Remove LON-SRV2 from $computers.
5. Display the contents of $computers.
6. Leave the Windows PowerShell prompt open for the next exercise.
Results: After completing this exercise, you should have manipulated arrays and arraylists.


Exercise 3: Using hash tables

Scenario

After using variables and arrays, you plan to practice working with hash tables.
The main tasks for this exercise are as follows:
1. Use a hash table.
2. Prepare for the next module.

Task 1: Use a hash table
1. Create a hash table named $mailList with the following users and email addresses:
o Frank - Frank@fabrikam.com
o Libby - LHayward@contoso.com
o Matej - MStojanov@tailspintoys.com
2. Display the contents of $mailList.
3. Display the email address for Libby.
4. Update the email address for Libby to Libby.Hayward@contoso.com.
5. Add a new email address for Stela: Stela.Sahiti@treyresearch.net.
6. View the count of items in $mailList.
7. Remove Frank from $mailList.
8. Verify that Frank is removed.
9. Close the Windows PowerShell prompt.

Exercise 4: Processing an array with a ForEach loop
Scenario
A. Datum is testing a new voice over IP (VoIP) and video conferencing system. To support this system, you
must set the ipPhone attribute for a group of test users. The naming convention that has been selected for
the ipPhone attribute is FirstName.LastName@adatum.com.
The main tasks for this exercise are as follows:
1. Create a test group.
2. Create a script to configure the ipPhone attribute.

Task 1: Create a test group
1. On LON-dc1, use PowerShell to create a new AD DS group named IPPhoneTest in the IT
organizational unit.
2. Add the following users as members in the IPPhoneTest group:
o Abbi Skinner

Task 2: Create a script to configure the ipPhone attribute
1. Create a script named c:\script\ipPhone.ps1, and then open it in the Windows
PowerShell ISE.
2. Use Get-ADGroupMember to create a query to obtain the membership of the IPPhoneTest group.
3. Create a ForEach loop that processes the users that are members of IPPhoneTest.
4. In the loop:
o Use Get-ADUser to retrieve the first and last names for a user.
o Calculate the required value for the ipPhone attribute.
o Use Set-ADUser with the -Replace parameter to set the ipPhone attribute for the user.
5. Run the script and then verify that the ipPhone attribute is modified for the selected users.
Results: After completing this exercise, you should have configured an Active Directory attribute by using
a ForEach loop.

Exercise 3: Processing items by using If statements

Scenario

Some of the servers in your organization have services that do not start properly when the server is
restarted. You want to create a script that can be used to start a specified list of services. When you have
performed sufficient testing, you plan to configure a scheduled task that runs the script. During the
testing phase, you will work with the Windows Time and Print Spooler services.
The main tasks for this exercise are as follows:
1. Create services.txt with service names.
2. Create a script that starts stopped services.

Task 1: Create services.txt with service names
1. On LON-dc1, open Windows PowerShell.
2. Create a new file c:\script\services.txt.
3. Identify the correct name for the Print Spooler service and add it to services.txt.
4. Identify the correct name for the Windows Time service and add it to services.txt.MCT USE ONLY. STUDENT USE PROHIBITED
Automating Administration with Windows PowerShell 8-25

Task 2: Create a script that starts stopped services
1. Create a new script c:\script\StartServices.ps1.
2. Retrieve the service names from services.txt and place them in a variable.
3. Use a ForEach loop to process each service:
o If the service is not running, start it and write text to the screen indicating that the service was
started.
o If the service is running, do nothing and write text to the screen indicating that no action was
required.
Results: After completing this exercise, you should have created a script that starts a list of services that
are defined in a text file.

Exercise 4: Creating a random password

Scenario

In this exercise, you will use a For loop to create a password composed of a specified number of random
characters and write it to the screen. The length of the password generated can be modified by updating
the value of a variable at the start of the script. You must generate random numbers and convert them to
characters.
The main task for this exercise is as follows:

1. Create a script that generates random passwords.

Task 1: Create a script that generates random passwords
1. Create a new script c:\script\CreatePasswords.ps1.
2. At the start of the script, set the variable $passwordLength to 8.
3. Use the For construct to create a loop that runs the number of times specified by $passwordLength.
o Generate a random number with a minimum value of 65 and maximum value of 90.
o Generate a letter from the random number by converting it to be a [char] variable.
o Add the letter to the $password variable.
4. Display the password on the screen.
Results: After completing this exercise, you should have created a script that generates a random
password.

Exercise 5: Creating users based on a CSV file

Scenario

In this exercise, you will import a CSV file and use the data to create user accounts in AD DS.
The main tasks for this exercise are as follows:
1. Create AD DS users from a CSV file.
2. Prepare for the next module.

Task 1: Create AD DS users from a CSV file
1. Create a new script named c:\script\CreateUsers.ps1.
2. Create users.csv and store the objects in a variable.
   Department,Login,first,last
3. Add custom rows to files csv
4. Create a ForEach loop that processes the data in the variable to create user accounts:
o Create a variable that contains the LDAP name of the organizational unit for the user. For
example: OU=IT,DC=Adatum,DC=com
o Create a variable that contains the user principal name for the new user. This should be in the
format UserID@adatum.com.
o Create a variable that contains the display name for the new user. This should be in the format of
FirstName LastName.
o Write a status message to the screen indicating which user is being created and where.
o Create the new user and be sure to set the following:
 GivenName
 Surname
 Name
 DisplayName
 SamAccountName
 UserPrincipalName
 Path
 Department

# Practice Lab: Configuring and Troubleshooting BitLocker

## Summary

In this lab you encrypt a local disk drive using BitLocker. You also troubleshoot access to a BitLocker encrypted drive when the user has forgot the password to unlock the drive.

## Exercise 1: Configuring BitLocker

### Scenario

You have a Windows 11 computer that has sensitive data stored on the D drive. You decide to configure and test BitLocker to see how it can be used to protect the data files that are stored on the local drive (D:).

### Task 1: Configure Active Directory Group Policy settings to support BitLocker

1. Sign in to **SEA-SVR1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. From Server Manager, select **Tools** and then select **Group Policy Management**.

3. Expand **Forest:Contoso.com**, and then expand **Domains**.

4. Right-click **Contoso.com** and then select **Create a GPO in this domain, and Link it here.**

5. In the **New GPO** box, under **Name** enter **BitLocker Policy** and then select **OK**.

6. Expand **Contoso.com**, right-click **BitLocker Policy**, and then select **Edit**.

7. In the Group Policy Management Editor, under **Computer Configuration**, expand **Policies**, expand **Administrative Templates**, expand **Windows Components**, and then select **BitLocker Drive Encryption**.

8. In the navigation area, expand **BitLocker Drive Encryption** and then select **Fixed Data Drives**.

9. Double-click **Configure how BitLocker-protected fixed drives can be recovered**.

10. Select **Enabled**, and then ensure that the check box next to **Save BitLocker recovery information to AD DS for fixed data drives** is selected, and then select **OK**.

11. In the navigation area, expand **BitLocker Drive Encryption** and then select **Operating System Drives**.

12. Double-click **Configure how BitLocker-protected operating system drives can be recovered**.

13. Select **Enabled**, and then ensure that the check box next to **Save BitLocker recovery information to AD DS for fixed data drives** is selected, and then select **OK**.

14. In the navigation area, expand **BitLocker Drive Encryption** and then select **Removable Data Drives**.

15. Double-click **Choose how BitLocker-protected removable drives can be recovered**.

16. Select **Enabled**, and then ensure that the check box next to **Save BitLocker recovery information to AD DS for fixed data drives** is selected, and then select **OK**.

17. Close the **Group Policy Management Editor** and the **Group Policy Management** console.


### Task 2: Enable BitLocker

1. Switch to and then restart SEA-CL1.

2. Sign in to SEA-CL1 as **Contoso\Administrator** with the password of **Pa55w.rd**.

3. On the taskbar, select the **File Explorer** icon.

4. In File Explorer, in the navigation pane, expand **This PC**.

5. In the navigation pane, right-click **Allfiles (D:)**, and then select **Turn on BitLocker**.

6. In the **BitLocker Drive Encryption (D:)** dialog box, select **Use a password to unlock the drive**.

7. In the **Enter your password** and **Reenter your password** boxes, type **Pa55w.rd**, and then select **Next**.

8. On the **How do you want to back up your recovery key?** page, select **Save to a file**.

9. In the **Save BitLocker recovery key as** dialog box, select **Documents** and then select **Save**. Select **Next**.

10. On the **Choose how much of your drive to encrypt** page, ensure that **Encrypt used disk space only (faster and best for new PCs and drives)** is selected, and then select **Next**.

11. On the **Choose which encryption mode to use** page, ensure that **New encryption mode (best for fixed drives on this device)** is selected, and then select **Next**.

12. On the **BitLocker Drive Encryption (D:)** page, select **Start encrypting**. Notice the lock icon next to the Allfiles (D:) node in the navigation bar, which indicates that the drive is currently unlocked.

13. Restart SEA-CL1.

### Task 3: Verify BitLocker

1. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. Select the **File Explorer** icon on the taskbar.

3. In File Explorer in the navigation pane expand **This PC**, and select **Allfiles (D:)**. Notice the lock icon next to Local Disk (D:). This indicates that the drive is protected by BitLocker.

4. In the BitLocker (D:) window, enter the password **Pa55w.rd**, press Enter to unlock the drive, and then verify access to the drive contents.

5. Right-click **Allfiles (D:)**, select **Show more options**, and then select **Manage BitLocker**. Take note of the options available for managing BitLocker on Allfiles (D:).

6. Select **Turn off BitLocker**.

7. In the BitLocker Drive Encryption dialog box, select **Turn off BitLocker**.

8. Close the BitLocker Drive Encryption window.

9. In File Explorer, notice that that lock icon is no longer visible next to Allfiles (D:).

10. Close all open windows and sign out of SEA-CL1.

**Results**: After completing this exercise, you will have configured BitLocker to encrypt a local disk drive.

## Exercise 2: Troubleshooting BitLocker

### Scenario

Jon has a Windows 11 computer that has sensitive data stored on the D drive. He has enabled BitLocker on drive D but has forgot the password to access the data. You need to determine how to access the recovery key and use it to unlock access to the drive content.


### Task 1: Enable BitLocker

1. Sign in to SEA-CL1 as **Contoso\Jon** with the password of **Pa55w.rd**.

2. On the taskbar, select the **File Explorer** icon.

3. In File Explorer, in the navigation pane, expand **This PC**.

4. In the navigation pane, right-click **Allfiles (D:)**, and then select **Turn on BitLocker**. At the User Account Control, enter **Administrator** with the password of **Pa55w.rd**.

5. In the **BitLocker Drive Encryption (D:)** dialog box, select **Use a password to unlock the drive**.

6. In the **Enter your password** and **Reenter your password** boxes, type **Pa55w.rd**, and then select **Next**.

7. On the **How do you want to back up your recovery key?** page, select **Save to a file**.

8. In the **Save BitLocker recovery key as** dialog box, select **Downloads** and then select **Save**. Select **Next**.

9. On the **Choose how much of your drive to encrypt** page, ensure that **Encrypt used disk space only (faster and best for new PCs and drives)** is selected, and then select **Next**.

10. On the **Choose which encryption mode to use** page, ensure that **New encryption mode (best for fixed drives on this device)** is selected, and then select **Next**.

11. On the **BitLocker Drive Encryption (D:)** page, select **Start encrypting**. 

12. Restart SEA-CL1.

### Task 2: Troubleshoot BitLocker

1. Jon's computer has the D: drive encrypted with BitLocker. He has returned from vacation and cannot remember the password to unlock and access the D drive. He needs to be able to access the files. You need to identify how to gain access to the locked drive and then change the password to one that he will remember. Attempt to resolve the problem by using your knowledge of BitLocker. If you are unable to resolve the problem, escalate it by asking your instructor for additional guidance. The following steps provide the troubleshooting steps and solution to the issue.

2. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

3. Select the **File Explorer** icon on the taskbar.

4. In File Explorer in the navigation pane expand **This PC**, and select **Local Disk (D:)**. 

5. In the BitLocker (D:) window, enter the password **password123**, and then select **Unlock**. You receive a message that the password is incorrect.

6. In the BitLocker (D:) box, select **More options**.

   > Take note of the **Enter recovery key** link. Where can you find a copy of the recovery key? Hint: Group policy settings were configured to ensure you can have access to the recovery key.

7. Switch to **SEA-SVR1**.

8. From Server Manager, select **Tools**, and then select **Active Directory Users and Computers**.

9. In Active Directory Users and Computers, expand **Contoso.com** and then select the **Seattle Clients** Organizational Unit.

10. Right-click SEA-CL1 and then select **Properties**.

11. In the SEA-CL1 Properties box, select the **BitLocker Recovery** tab.

12. Right-click the most recent BitLocker Recovery Password, and then select **Copy Details**.

13. On the taskbar, open **File Explorer** and then browse to **\\\\SEA-CL1\\C$**.

14. Create a new text document and paste the BitLocker details into the document. Save the document.

15. Close all open windows and then sign out of SEA-SVR1.

16. Switch to SEA-CL1.

17. In File Explorer, select **Local Disk (C:)** and then open the text document that contains the Recovery password.

18. Under Recovery Password, arrange the 48 numbers to ensure that the password is on a single line.

19. Copy the 48 number recovery password.

20. Switch to File Explorer and then select **Allfiles (D:)**.

21. At the BitLocker (D:) box, select **More options** and then select **Enter recovery key**.

22. Paste the recovery key and then select **Unlock**.

23. Browse to D: Drive and verify that you can access the files.

24. Right-click **Allfiles (D:)**, select **Show more options**, and then select **Change BitLocker password**. 

25. On the BitLocker Drive Encryption box, select **Reset a forgotten password**.

26. In the BitLocker Drive Encryption box, enter **Pa55w.rd** for both the Enter your password and Reenter your password fields.

27. Select **Finish** and then select **OK**. The drive has now been recovered and you have reset the password.

### Task 3: Turn off BitLocker

1. In File Explorer in the navigation pane expand **This PC**, and select **Allfiles (D:)**. 

2. Right-click **Allfiles (D:)**, select **Show more options**, and then select **Manage BitLocker**.

3. Select **Turn off BitLocker**.

4. In the BitLocker Drive Encryption dialog box, select **Turn off BitLocker**.

5. Close the BitLocker Drive Encryption window.

6. Close all open windows and sign out of SEA-CL1.


**Results**: After completing this exercise, you will have configured BitLocker and recovered access using a recovery key.

**END OF LAB**

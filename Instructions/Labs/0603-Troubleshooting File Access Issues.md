# Practice Lab: Troubleshooting File Access Issues

## Summary

In this lab, you will troubleshoot and resolve permissions needed to access file resources.

## Lab Setup

### Task 1: Simulate the issue

1. Sign in to **SEA-SVR2** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. Open **File Explorer** and then browse to **E:\\Labfiles\\Mod07**.

3. Run the **E:\\Labfiles\\Mod07\\Lab.cmd** script.

4. Close File Explorer.

## Exercise 1: Resolving file permissions

### Scenario

Users in the Marketing department have a data folder to which they should have exclusive access.  

Alice Ciccu, a member of the Marketing department, reports that non-Marketing users have access to Marketing data in the **\\\\SEA-SVR2\\Marketing** shared folder. 

Mike Ray, a member of the IT department, reports that he can review and open files in the Marketing share, but cannot modify the files in this share.

You need to investigate and ensure that only members of the Marketing department can access the the **\\\\SEA-SVR2\\Marketing** shared folder.

### Task 1: Validate the issue

1. Sign in to **SEA-CL1** as **Contoso\\Mike** with the password **Pa55w.rd**.

2. From the taskbar, open the **File Explorer**.

3. In File Explorer, in the address bar, enter **\\\\SEA-SVR2\\Marketing**, and then select Enter.

4. In the details pane, open **Report**, and then verify that it opens in Notepad.

5. In Notepad, enter your name. Select **File**, select **Save**, select **Report**, select **Save**, and then select **Yes**.

   > You will receive a message that indicates “You do not have permission to open this file”, because Mike is not in the Marketing group and he cannot modify the files.

6. In the message select **OK**, close **Notepad**, and then select **Don’t Save**.

   > Mike is not in the Marketing group, so you should not be able to access the share. However, you were able to open share content. You need to diagnose and correct this improper configuration.

7. Close File Explorer and sign out of SEA-CL1.

### Task 2: Resolve the issue

1. Users who are not members of the Marketing group should not be able to access the Marketing share. Attempt to resolve the problem by using your knowledge of file permissions and shared folder access. If you are unable to resolve the problem, escalate it by asking your instructor for additional guidance. The following steps provide the troubleshooting steps and solution to the issue.

2. Sign in to **SEA-SVR2** as **Contoso\\Administrator** with the password **Pa55w.rd**.

3. Open **File Explorer** and then browse to **E:\\**.

4. Right-click **Marketing** or activate its context menu, and then select **Properties**.

5. In the Marketing Properties dialog box, select the **Sharing** tab.

6. On the Sharing tab, select **Advanced Sharing** and then select **Permissions**. Verify that the permissions are granted to Everyone Change, and then select Cancel twice.

7. In the Marketing Properties dialog box, select the **Security** tab.

8. On the Security tab, select **Advanced**, and then select the **Effective Access** tab.

9. On the Effective Access tab, select **Select a user**. 

10. In the Select User, Computer, Service Account, or Group dialog box, enter **Mike**, click **Check Names** and then select **OK**, and then select **View effective access**.

11. Verify that Mike has Read permissions, but he does not have Change or Delete permissions, and then select the **Permissions** tab.

12. In the Advanced Security Settings for Marketing dialog box, select **Disable inheritance**.

13. Select **Convert inherited permissions into explicit permissions on this object,** and then select **OK**.

14. In the **Marketing Properties** dialog box, select **Edit**.

15. In the Permissions for Marketing dialog box, select **Users**, select **Remove**, and then select **OK**. 

16. Select **Advanced**, and then select the **Effective Access** tab.

17. On the Effective Access tab, select **Select a user**. 

18. In the Select User, Computer, Service Account, or Group dialog box, enter **Mike**, click **Check Names** and then select **OK**, and then select **View effective access**. Verify that Mike has no permissions.

19. On the Effective Access tab, select **Select a user**. 

20. In the Select User, Computer, Service Account, or Group dialog box, enter **Alice**, click **Check Names** and then select **OK**, and then select **View effective access**. 

21. Verify that Alice is a member of the Marketing group, that she has Read and Write permissions, and that her access is limited only by share permissions. 

22. Select **OK**, and then select **Close**. 

    > The inherited permissions on E:\Marketing included the Users group having Read permissions. The Users group was removed, and now only members of the Marketing group have access.

25. Close all open windows and sign out of SEA-SVR2.

**Results**: After completing this exercise you have fixed file permission issues for the Marketing department.

## Exercise 2: Resolving file access

### Scenario

Some Marketing users can modify files in the Collected folder on the Marketing share and some Marketing users cannot.  

Bruce Keever, is a member of the Marketing department and located in London. He reports that he and some other Marketing users cannot modify the **Survey.txt** file in the Collected folder on the Marketing share. He can open the file and read its content.

Alice Ciccu is also a member of Marketing department and located in Seattle. She reports that she is able to modify the Survey.txt file. 

You need to investigate and ensure that all users from the Marketing department from both Seattle and London offices be able to modify the files in the Collected folder.

### Task 1: Validate the issue

1. Sign in to **SEA-CL1** as **Contoso\\Alice** with the password **Pa55w.rd**.

2. From the taskbar, open the **File Explorer**.

3. In File Explorer, in the address bar, enter **\\\\SEA-SVR2\\Marketing\\Collected**, and then select Enter.

4. In the details pane, open **Surveys**, and then verify that it opens in Notepad.

5. In Notepad, enter your name, close **Notepad**, and then select **Save**.

   > You now have verified that Alice can modify the file.

6. Close File Explorer and sign out of SEA-CL1.

7. Sign in to **SEA-CL1** as **Contoso\\Bruce** with the password **Pa55w.rd**.

8. From the taskbar, open the **File Explorer**.

9. In File Explorer, in the address bar, enter **\\\\SEA-SVR2\\Marketing\\Collected**, and then select Enter.

10. In the details pane, open **Surveys**, and then verify that it opens in Notepad.

11. In Notepad, enter some additional text, close **Notepad**, select **Save**, select **Surveys**, select **Save** again, and then select **Yes**.

    > This message displays because Bruce does not have permission to modify the file.

12. In Notepad, select **OK**. Select **Cancel**, close **Notepad**, and then select **Don’t Save**

13. Close File Explorer and sign out of SEA-CL1.

### Task 2: Resolve the issue

1. Marketing users who are from offices in Seattle and London must be able to modify the files in the Collected folder. Attempt to resolve the problem by using your knowledge of file permissions and shared folder access. If you are unable to resolve the problem, escalate it by asking your instructor for additional guidance. The following steps provide the troubleshooting steps and solution to the issue.

2. Sign in to **SEA-SVR2** as **Contoso\\Administrator** with the password **Pa55w.rd**.

3. Open **File Explorer** and then browse to **E:\\Marketing\\Collected**.

4. In the details pane, right-click **Surveys.txt** or activate its context menu, select **Properties**, select the **Security** tab, and then select **Advanced**.

5. In Advanced Security Settings for Surveys.txt, verify that there is a condition defined for Allow Write access for the Marketing group. Confirm that the condition requires that the user's city is Seattle.

6. Select the **Effective Access** tab. Select **Select a user**, enter **Bruce**, click **Check Names** and then select **OK**, and then select **View effective access**.

7. Review effective access for Bruce.

   > Bruce has Read permissions, but permissions do not allow him to write data to the file. This is because you did not include a user claim yet, so the condition was not evaluated for Bruce.

8. Select **Include a user claim**, select the drop-down box arrow, and then select **City**. In the **Enter value here** text box, enter **Seattle**, and then select **View effective access**. 

9. Verify that if Bruce has a user claim for city with the value Seattle, and that he can write data to the file.

10. Select **Select a user**, enter **Alice**, click **Check Names** and then select **OK**.

11. Verify that user claim City=Seattle is still included, and then select **View effective access**.

12. Verify that if Alice has a user claim for city with a value of Seattle, she would also be able to write data to the file. Select **OK** twice.

    > You need to ensure that only Marketing users from offices in Seattle and London should be able to modify the file. Therefore, you must not remove the condition, but extend it to include Marketing users from London.

13. In File Explorer, in the navigation pane, right-click **Collected** or activate its context menu, and then select **Properties**. 

14. Select the **Security** tab, and then select **Advanced**.

15. In the Advanced Security Settings for Collected dialog box, select the Allow Write entry access for the Marketing group that has the Condition, and then select **Edit**.

16. In the Permission Entry for Collected dialog box, select **Add a condition**. In the drop-down box, expand the **And** option, and then select **Or**. 

16.	Compose the following expression: **User city Equals Value London**. You must enter London in the last text box, and then select **OK** three times.

17. Close all open windows and sign out of SEA-SVR2.

18. Switch to **SEA-CL1**.

19. Sign in to **SEA-CL1** as **Contoso\\Bruce** with the password **Pa55w.rd**.

20. From the taskbar, open the **File Explorer**.

21. In File Explorer, in the address bar, enter **\\\\SEA-SVR2\\Marketing\\Collected**, and then select Enter.

22. In the details pane, open **Surveys**, and then verify that it opens in Notepad.

23. In Notepad, enter some additional text, close **Notepad**, select **Save**.

    > Notice that Bruce can now modify the file, although he is from the London office.

24. Close File Explorer and sign out of SEA-CL1.

**Results**: After completing this exercise you have fixed the file access issue for the Marketing department.

**END OF LAB**

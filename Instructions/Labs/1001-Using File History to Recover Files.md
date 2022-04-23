# Practice Lab: Using File History to Recover Files

## Summary

In this exercise you configure File History and use it to restore previous versions of a file or folder.

## Exercise 1: Configuring File History

### Scenario

You need to ensure that users can recover deleted files stored in the Documents library on their local workstations. You decide to validate the File History feature using SEA-CL2. You will first create a shared folder on SEA-SVR1 named FileHistory to be used as a central storage location. You will then configure the File History feature on SEA-CL2 to store file history data.

### Task 1: Create a shared folder to store File History data

1. Sign in to **SEA-SVR1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. From the taskbar, select **File Explorer** and in the navigation pane, select **Local Disk (C:)**.

3. In File Explorer, in the details pane, right-click an empty space, point to **New**, and then select **Folder**. Type **FileHistory** as the folder name, and then press Enter.

4. Right-click the **FileHistory** folder, and then select **Properties**.

5. In the **FileHistory Properties** dialog box, on the **Security** tab, select **Edit**. Select **Add**, in the **Enter the object names to select** box, type **Domain Users**, and then select **OK**.

6. Select **Domain Users**, and in the **Permissions for Domain Users** section, in the Allow column, select the **Full control** check box, and then select **OK**.

8. On the **Sharing** tab, select **Advanced Sharing**.

9. Select the **Share this folder** check box, and then select **Permissions**. In the **Permissions for Everyone** section, in the Allow column, select **Full Control**, and then select **OK** twice.

10. In the **FileHistory Properties** dialog box, select **Close**.

11. Close File Explorer.

12. Sign out of SEA-SVR1.

### Task 2: Configure and test File History

1. Switch to **SEA-CL2** and sign in as **Contoso\\Administrator**, with the password **Pa55w.rd**.

2. On **SEA-CL2**, on the taskbar, select **File Explorer**.

3. In File Explorer, in the navigation pane, expand **This PC**, and then select **Documents**. In the details pane, right-click an empty space, point to **New**, select **Text Document**, and then enter **Report** as the name of the file.

4. Double-click **Report.txt**, and in Notepad, type **This is a report**. Close the Notepad file, and then select **Save** to save the changes.

5. Select **Start**, type **file history**, and then select **Restore your files with File History**.

6. In the **Home – File History** window, select **Configure File History settings**.

7. In the **File History** window, in the navigation pane, select **Select drive**.

8. In the **Select Drive** dialog box, select **Add network location**.

9. In the **Folder** box, type **\\\\SEA-SVR1\\FileHistory**, select **Select Folder**, and then select **OK**.

10. In the **File History** window, in the details pane, select **Turn on**.

11. In the navigation pane, select **Advanced settings**, review the default values for how often to save copies of files and how long to keep saved versions, and then select **Cancel**.

12. In File Explorer, in the navigation pane, select **Documents**, right-click **Report.txt**, and then select **Delete**.

13. In File Explorer, in the navigation pane, right-click **Documents**, select **Show more options**, and then select **Restore previous versions**.

14. In the Documents Properties window, select the **Previous Versions** tab.

    > Notice that the Previous Versions tab displays the Documents file that was previously deleted. 

15. On the Previous Versions tab, select the arrow next to **Open** and then select **Open in File History**.

16. In the Documents-File History window, right-click **Report.txt** and then select **Preview**. Verify that the file contains the text you entered when the file was created.

17. In the Documents-File History window, select the **Restore to original location** button.

18. File Explorer opens. Verify that Report.txt has been restored to the original location and then close File Explorer.

19. In the Report.txt – File History window, on the left of the address box, select the upward-pointing arrow twice.

20. Review the folders and libraries that File History is protecting, and confirm that the a folder named Data and a folder named Reports are not among them.

    > File history protects a number of default folders and libraries. For custom folders you need to include them in the library as shown in the next exercise.

21. Close the **Home – File History** window.

22. Close all open windows on SEA-CL2.

**Results**: After completing this exercise, you will have successfully configured File History and validated a successful recovery of a protected file.

## Exercise 2: Protecting Custom Folders using File History

### Scenario

A request has been made to use File History to protect two custom folders on SEA-CL2 named Data and Reports.  Both folders need to be added to the Documents library to be protected by File History.

### Task 1: Configure the lab environment

> This task is needed to create the folder structure to be used in the lab scenario.

1. On **SEA-CL2**, open File Explorer, and then browse to **\\\\SEA-DC1\\labfiles\\Support\\**.

2. In the content pane, double-click **CopyUserData.bat** to copy lab files to the local client.

3. In File Explorer, in the navigation pane, expand **Local Disk (C:)**, and then select **Data**. In the details pane, right-click **Sales.txt**, select **Properties**, select the **Previous Versions** tab, confirm that there are no previous versions available, and then select **OK**.

### Task 2: Configure File History to protect custom folders

1. In the navigation pane, right-click **Data**, select **Show more options**, point to **Include in library**, and then select **Documents**. 

   > As File History protects the Documents library, File History is now also protecting the Data folder.

2. In File Explorer, in the navigation pane, select **Reports**. In the details pane, right-click **Report.txt**, select **Properties**, select the **Previous Versions** tab, confirm that there are no previous versions available, and then select **OK**.

3. In the navigation pane, right-click **Reports**, select **Show more options**, point to **Include in library**, and then select **Documents**.

4. Select **Start**, type **file history**, and then select **File History**.

5. In the **File History** window, in the **File History is on** section, select **Run now**.

6. In File Explorer, in the details pane, right-click **Report.txt**, select **Properties**, select the **Previous Versions** tab, verify that there is now one previous version, and then select **OK**.

7. In the navigation pane, right-click **Data**, select **Properties**, select the **Previous Versions** tab, and then select **Data** in the **Folder versions** section.

8. Select the arrow near the **Restore** button, and then verify that you can restore the previous version either to the original location or to a custom location.

9. In the **Data Properties** dialog box, select the arrow near the **Open** button, and then select **Open in File History**.

10. In the Data – File History window, on the left of the address box, select the upward-pointing arrow once. 

    > Notice that File History is protecting the Data and Reports folders, in addition to the Users folder, which is protected by default.

11. In the C:\\ - File History window, select the upward-pointing arrow again to view all folders and libraries that File History is protecting.

12. Close the Home – File History window, in the **Data Properties** dialog box, select **OK**.

13. Close all open windows and sign out of SEA-CL2.

**Results**: After completing this exercise, you will have successfully added additional folders to be protected by using File History.

**END OF LAB**

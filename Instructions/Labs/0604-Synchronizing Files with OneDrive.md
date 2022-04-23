# Practice Lab: Synchronizing files with OneDrive

## Summary

In this lab you will learn how to synchronize content between devices using OneDrive.

### Scenario

Your organization would like to leverage OneDrive as a method for accessing user files from any device. You test this solution by signing in with your Microsoft account and creating a file on SEA-WS2 and verifying that the file automatically synchronizes to SEA-WS1. You will also enable OneDrive PC folder backup to redirect the local Desktop and Documents folder to OneDrive.

*Note: To complete this lab, you need to have a Microsoft account. You can obtain a free Microsoft account which can be created at <https://outlook.live.com>. Your instructor can guide you on how to create an account if required.*

### Task 1: Connect your Microsoft account to SEA-WS1 and SEA-WS2

1. Sign in to **SEA-WS1** as **Student** with the password **Pa55w.rd**.

2. Select **Start** and then select **Settings**.

3. In the **Settings** page, select **Accounts**.

4. On the **Accounts** page, select **Your info**.

5. Select the link that states **Sign in with a Microsoft account instead**.

6. In the **Microsoft account Sign in** page, enter your Microsoft account email address and then select **Next**.

7. On the **Enter password** page, enter your Microsoft account password and then select **Sign in**.

8. In the **Sign into this computer using your Microsoft account** page, enter **Pa55w.rd** and then select **Next**.

9. On the **Create a PIN** page, select **Next**.

10. In the **Set up a PIN** dialog box, enter **1029** in both the **New PIN** and **Confirm PIN** boxes. Select **OK**. Notice that your Microsoft account is now listed on the Your info page.

11. Sign out of SEA-WS1.

12. Repeat steps 1-11 on SEA-WS2.

### Task 2: Enable OneDrive sync on SEA-WS2

1. Sign in to **SEA-WS2** with your Microsoft account and the PIN **1029**.

2. On the task bar, select **File Explorer**, and then select the **OneDrive** node.

_**Note**: The OneDrive node in File Explorer might take several minutes to appear. Please wait for it to appear before proceeding. If it takes longer than 15 minutes, sign out, and then sign back in by using your Microsoft account. If you are prompted to provide your email address, use the Microsoft account that you signed in with._

3. In the File Explorer console tree, expand **OneDrive**, and then select the **Documents** folder.

    *If the Documents folder is not visible, wait approximately 5 minutes for it to appear.*

4. Right-click the empty space in the **Details pane**, select **New**, and then select **Text Document**.

5. Type **File from SEA-WS2** in the **Name** box, and then press Enter.

6. Double-click the document, and when Notepad opens, type **File on SEA-WS2**. Press **Ctrl+S**, and then close Notepad.

7. Wait until OneDrive has synchronized the changes indicated by a green check mark symbol in the **Status** row.

_**Note**: If OneDrive indicates it is paused, right-click on the OneDrive status icon, select Resume Syncing._

### Task 3: Enable OneDrive sync on SEA-WS1

1. Switch to **SEA-WS1**.

2. Sign in to **SEA-WS1** with your Microsoft account with the PIN **1029**.

3. On the task bar, select **File Explorer**, and then select the **OneDrive** node.

4. In the **File Explorer** console tree, expand **OneDrive**, and then select the **Documents** folder. After a few minutes, the **File from SEA-WS2** document should appear (it can take up to five minutes).

    _**Note**: By default OneDrive has the Files On-Demand feature enabled that will download files only on the first use on a device. Such cloud files that have been created Online or on another device are indicated by a cloud symbol in Status._

5. Double-click the **File from SEA-WS2** document.  

    _**Note**: The file will now be downloaded to your device before it will open. If OneDrive indicates it is paused, right-click on the OneDrive status icon, select Resume Syncing._

6. In the **Notepad** window, directly under the **File on SEA-WS2** line, type **Also on SEA-WS1**, and then press **Enter**.

7. Press **Ctrl+S**, and then close Notepad.

8. Make a note of the date and time of the **File from SEA-WS2** file.

9. On SEA-WS1, close File Explorer.

10. Switch to **SEA-WS2**.

11. Check the date and time of the **File from SEA-WS2** document. When it changes to the date and time you noted on **SEA-WS1**, double-click the file (it takes up to five minutes to change).

     _**Note**: You should now see the two lines in Notepad._

12. Close Notepad.

13. Right-click the **File from SEA-WS2** document, and select **Always keep on this device.**  

     _**Note**: The check mark symbol in Status will now change to a white check mark in a green circle indicating that this file is always available on your device._

14. Right-click the **File from SEA-WS2** document, and select **Free up space.**  

     _**Note**: This will convert the file back to an online document indicated by the cloud symbol that needs to be downloaded on the first use. This is intended to free up space on your local hard disk._

15. On SEA-WS2, close File Explorer.

### Task 4: Configure OneDrive PC folder backup 

1. Switch to SEA-WS1.

2. On SEA-WS1, select **Start** and then select **Settings**.

3. In the **Settings** page, select **Accounts**.

4. On the **Accounts** page, select **Windows backup**.

   > Notice that OneDrive folder backup is not enabled.

5. Next to OneDrive folder syncing, select **Set up syncing**. The Manage folder backup window opens.

   > Notice that you can choose to have OneDrive back up the desktop, Documents, and Pictures folders.

6. In the Manage folder backup dialog box, select **Desktop** and **Documents**. Remove the check mark next to **Pictures**.

7. Select **Start backup** and then select **View sync process**.

8. In the OneDrive app, select **Open folder**.

   > Notice the folders synced to OneDrive.

9. Close all open windows on SEA-WS1.

10. On SEA-WS1, on the desktop create a new Text document named **File1.txt**.

11. Repeat steps 1-9 on SEA-WS2.

    > Notice File1.txt is synchronized to the desktop on SEA-WS2. Desktop and Documents are synchronized and available from both SEA-WS1 and SEA-WS2.

13. Sign out of both SEA-WS1 and SEA-WS2.

**Results**: During this lab you have synchronized files between different devices using OneDrive.

**END OF LAB**

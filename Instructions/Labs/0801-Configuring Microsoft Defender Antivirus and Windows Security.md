# Practice Lab: Configuring Microsoft Defender Antivirus and Windows Security

## Summary

In this exercise you will configure Microsoft Defender Antivirus and Windows Security settings.

## Exercise 1: Detecting threats using Microsoft Defender Antivirus

### Scenario

You've been asked to configure and test Microsoft Defender Antivirus on SEA-CL1. You need to configure protection settings to enable controlled folder access and ensure that Microsoft Defender can detect vulnerabilities. You've decided to simulate a virus using a test file, sample.txt, located at C:\Files, to validate successful threat detection. You will also test out exclusions to see how adding an exclusion changes the behavior of the virus scanning process.

### Task 1: Configure Microsoft Defender Antivirus

1. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. Select **Start**, and then select the **Settings** icon.

3. In the Settings window, select **Privacy & security**, and then select **Windows Security**. Take note of the Protection areas listed under Windows Security.

4. Select **Open Windows Security**.

5. In Windows Security, select **Virus & threat protection**.

6. On the Virus & threat protection page, under Virus & threat protection settings, select **Manage settings**.

7. Under Controlled folder access, select **Manage Controlled folder access**.

8. On the Ransomware protection page, enable **Controlled folder access**.

9. Under Controlled folder access, select **Protected folders** to view the default folders that are protected from unauthorized changes.

10. In the navigation pane, select **Virus & threat protection**.

### Task 2: Perform a scan

1. On the Virus & threat protection page, select **Scan options**.

2. Take note of the options available to configure and then select **Quick scan** and then select **Scan now**.

3. The quick scan begins and provides information on the number of files scanned and estimated time remaining. The final result should state **No current threats**.

4. In the navigation pane, select **Virus & threat protection**.

5. Close the Windows Security window and close Settings.

### Task 3: Introduce suspicious software

1. On the task bar, select the **File Explorer** icon.

2. In **File Explorer** browse to **C:\\Files**.

3. In the Files folder, double-click **sample.txt**.  

   _**Note**: The sample.txt file contains a text string to test malware detection._

4. In the sample.txt file, **delete** both instances of **remove** including the brackets and any extra lines or blank spaces.

5. Select **Save** and close Notepad.

   _**Note**: Microsoft Defender will immediately detect a potential threat and remove the file. It may take a minute for the file to automatically be removed._

### Task 4: View the quarantined file ###

1. In the notification area, select the **Notifications** icon, and then in the Action Center, select the notification that states that **Threats found**.

   _**Note**: This will open the **Virus & threat protection** page in Windows security. The file is quarantined now._

2. Under Current threats, select **Protection history**.

3. Take note of and select the **Threat quarantined** item.

4. Read the information about the threat and then select the **Actions** button and then select **Remove**.

5. Close all open windows.

### Task 5: Configure exclusions ###

1. From the taskbar, open **File Explorer**.

2. Browse to **\\\\SEA-DC1\\Labfiles\\Threat**.

3. Copy the **sample.txt** file and paste it to **C:\Files**.

4. Close File Explorer.

   > The above task has replaced the sample virus file in the C:\Files folder. You will now configure an exclusion for the C:\Files folder and validate the behavior of the virus scan.

5. Select **Start**, and then select the **Settings** icon.

6. In the Settings window, select **Privacy & Security**, and then select **Windows Security**.

7. Select **Open Windows Security**.

8. In Windows Security, select **Virus & threat protection**.

9. On the Virus & threat protection page, under Virus & threat protection settings, select **Manage settings**.

10. Under Exclusions, select **Add or remove exclusions**.

11. On the Exclusions page, select **Add an exclusion** and then select **Folder**.

12. Browse to **C:\Files** and then click **Select Folder**. The excluded folder is shown on the Exclusions page.

13. Close **Windows Security** and then close **Settings**.

### Task 6: Validate the excluded folder

1. On the task bar, select the **File Explorer** icon.

2. In **File Explorer** browse to **C:\\Files**.

3. In the Files folder, double-click **sample.txt**.  

   _**Note**: The sample.txt file contains a text string to test malware detection._

4. In the sample.txt file, **delete** both instances of **remove** including the brackets and any extra lines or blank spaces.

5. Select **Save** and close Notepad.

   > Notice that you do not receive any notification from Microsoft Defender. Because this folder is excluded, it will not be protected by the antivirus process.

6. Close all open windows.

**Results**: After completing this exercise, you will have configured and tested Microsoft Defender Antivirus.

## Exercise 2: Configuring Windows Security Settings

### Scenario

You need to verify that Microsoft Defender SmartScreen has been enabled and is configured on SEA-CL1. You also need to verify that Exploit Protection settings are On by default.

### Task 1: Configure Windows Security

1. On SEA-CL1, select **Start**, and then select the **Settings** icon.

2. In the Settings window, select **Privacy & security**, and then select **Windows Security**. 

3. Select **Open Windows Security**.

4. In Windows Security, select **App & browser control**.

5. On the App & browser control page, under Reputation-based protection, select **Reputation-based protection settings**.

6. Verify that Microsoft Defender SmartScreen has been enabled for apps, files, Microsoft Edge, and Microsoft Store apps.

7. Under Potentially unwanted app blocking, select the check box to enable **Block downloads**.

8. Click **Back** to return to the App & browser control page.

9. Under Exploit protection, select **Exploit protection settings**.

10. Verify that System settings are all configured to **Use default (On)**.

11. Close the Windows Security window.

12. Sign out of SEA-CL1.

**Results**: After completing this exercise, you will have verified settings related to Microsoft Defender SmartScreen and Exploit protection.

**END OF LAB**

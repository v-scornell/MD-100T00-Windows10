# Practice Lab: Managing Windows Settings

## Summary

In this lab you will validate and configure Windows 11 by using Windows Settings, the Control Panel, and Windows PowerShell. 

## Exercise 1: Configuring Settings Using Windows Settings and Control Panel

### Scenario

You need to validate device and Windows specifications, configure various Windows 11 settings, and determine which applications are slowing down the Windows startup process. You also need to modify Focus assist settings to change how app notifications are received during non-working hours. Finally, you need to create a new power plan that minimizes power usage, but does not impact multimedia presentations while the device is running on battery.

### Task 1: Validate and configure Windows Settings

1. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. Select **Start** and then select the **Settings** icon.

3. In **Settings**, select **System**, and then select **About**. Take note of the Device specifications and Windows specifications.

4. Select **System**, and then select **Clipboard**. Take note of the Clipboard options, such as enabling clipboard history, syncing across devices, and clearing the clipboard data.

5. Next to **Clipboard history**, select the slider to enable the feature.

6. Select **System**, and then select **Storage**. Take note of the storage information including how storage is used on the device and features to use for storage management.

7. Under **Storage management**, select **Storage Sense**.

8. Under **Automatic User content cleanup**, select the slider to enable the feature. Take note of the additional cleanup schedules for Storage Sense.

9. Select **System**, and then select **Multitasking**. Take note of configuration options related to the Snap feature, Alt + Tab, and the use of multiple desktops.

10. In **Settings**, select **Apps**, and then select **Apps & features**. Take note of the Apps & features installed on the device.

11. Select **Apps**, and then select **Startup**. Take note of the apps that are configured to start when you sign in to the device.

12. Close **Settings**.


### Task 2: Configure Focus assist settings

1. On SEA-CL1, select **Start** and then select the **Settings** icon.

2. In **Settings**, select **System**, and then select **Notifications**. 

3. Expand **Notifications** and take notice of the options that are enabled.

4. Select **Focus assist.**

5. Under **Focus assist**, take note of the default setting. Focus assist is off except for when an Automatic rule is active.

6. Select the check box next to **Show a summary of what I missed with focus assist was on**.

7. Under **Automatic rules**, select the rule named **During these times**. 

8. On the **During these hours** page, enable the feature and select the check box next to **Show a notification in action center when focus assist is turned on automatically**. This will ensure that only Priority notifications are received during 11:00 PM and 7:00 AM and a notification is visible that the feature is active.

9. Close **Settings**.


### Task 3: Configure Power Options using the Control Panel

1. Select **Start** and type **Control Panel**. Press **Enter**.

2. In the Control Panel window, select **Hardware and Sound** and then select **Power Options**.

3. Select **Create a power plan.**

4. In the **Plan name** box, enter **Power Save - Presentation** and select **Next**.

5. Select **Create**.

6. Under **Preferred plans**, next to **Power Save - Presentation**, select **Change plan settings**.

7. Select **Change advanced power settings**.

8. Expand **Hard disk** and then expand **Turn off hard disk after**. Change the setting to **60** minutes.

9. Scroll down and expand the **Multimedia settings** option.

10. Expand the **When playing video** option and change the setting to **Balanced**.

11. Select **OK** to close the **Power Options** dialog box.

12. Close all open windows.

**Results:** After finishing this exercise you will have configured settings using Windows Settings and the Control Panel.

## Exercise 2: Using PowerShell to Configure Windows

### Scenario

You need to use Windows PowerShell to test the scripting environment. To become familiar with PowerShell you will run several commands and the use PowerShell ISE to create a script to list all running services on the device.

### Task 1: Use Windows PowerShell to configure a device

1. On SEA-CL1, select **Start** and type **PowerShell**. Select **Run as administrator**.

2. At the PowerShell window, type the following and then press **Enter**:

```
Get-ExecutionPolicy
```

3. Confirm the current setting of the PowerShell execution policy is set to **Unrestricted**.

4. If the execution policy is set to **Restricted**, change it to **Unrestricted** by running the following command at the PowerShell window:

```
Set-ExecutionPolicy Unrestricted
```

5. At the confirmation prompt, type **Y** and then select **Enter**.

6. Confirm that the execution policy is now **Unrestricted**.

7. At the PowerShell window, launch Notepad by typing the following command and then press **Enter**:

```
Start-Process Notepad
```

8. At the PowerShell window, type the following command and then press **Enter**:

```
Get-Process
```

9. Review the list of all running processes. Identify that Notepad is running and note the Process ID.

10. At the PowerShell window, type the following command and then press **Enter**. Replace [ID] with the Process ID identified in step 9.

```
Stop-Process -Id [ID]
```
11. Verify that the Notepad window is no longer open.

13. At the PowerShell window, list the event logs by typing the following command and then press **Enter**:

```
Get-EventLog -List
```

14. At the PowerShell window, list the application log entries by typing the following command and then press **Enter**:

```
Get-EventLog -LogName Application
```

15. At the PowerShell window, clear the application log entries with a confirmation by typing the following command and then press **Enter**:

```
Clear-EventLog -LogName Application -confirm
```

16. At the PowerShell window, verify that  the application log entries have been removed by typing the following command and then press **Enter**:

```
Get-EventLog -LogName Application
```

17. Select **Start** and type **Telnet**. Select **Turn Windows features on and off**.

18. In the **Windows Features** window, verify that **Telnet Client** is not selected.

19. At the PowerShell Window, type the following command, and then press **Enter**:

```
Enable-WindowsOptionalFeature -Online -FeatureName TelnetClient
```

_Note: This will install the Telnet Client windows feature._

20. Select **Start** and type **Telnet**. Select **Open**.

21. Close all open windows.

### Task 2: Use a Windows PowerShell Script

1. Select **Start** and then in the **Type here to search** box, type **\\\SEA-DC1\\Labfiles** and then press **Enter**.

2. In the content pane, double-click the **Configure** folder.

3. Copy the **Services.ps1** file into the **D:\\Labfiles** folder on SEA-CL1.

4. Select **Start** and type **Powershell ISE**. Press **Enter**.

5. In the Windows PowerShell ISE, open the script file **D:\\Labfiles\\Services.ps1**.

6. Review the script and note the formatting as follows:

   - Comments are green.
   - Variables are red.
   - Cmdlets are bright blue.
   - Text in quotation marks is dark red.

7. Review the script and note that after the script runs, all services that have the status of **Running** will display in green color. All services that do not have a status of Running will display in red color.

8. Select line 3 in the script, and then select **Run selection (F8)**.

   _Note: Only the command in line 3 will be executed._

9. Select **Run script (F5)**, and then read the output.

   _Note: The output does not have multiple colors, because the script needs to be modified to provide that information._

10. At the end of line 14, type **–ForegroundColor $color**

11. On the toolbar, select **Run script (F5)** in the Windows PowerShell ISE window. Select **OK** to save the file, and then read the output.

    _Note: Running services are green, and services that are not running are red._

12. On line 16, type **Write-Host "A total of" $services.count "services were evaluated"**

13. Select **Run script (F5)**, and in the Windows PowerShell ISE window select **OK**.

14. If necessary, select **Show Command Add-on** in the PowerShell ISE toolbar.

15. In the **Commands** pane, select the **Write-Host** cmdlet and then configure the following options:

    - BackgroundColor: **Gray**

    - ForegroundColor: **Black**

    - Object: **"Script execution is complete"**

16. Select **Copy** and paste the command to line 17 of the script.

17. Select **Run script (F5)**, and in the Windows PowerShell ISE window select **OK**.

18. Select **Start** and type **PowerShell**. Press **Enter**.

19. At the PowerShell window, type the following command and then press **Enter**:

```
Set-Location D:\Labfiles
```

20. At the PowerShell window, type the following and then press **Enter**:

```
.\Services.ps1
```

21. Close all open windows and sign out of SEA-CL1.

**Results:** After completing the exercise you will have managed Windows using PowerShell and PowerShell scripts.

**END OF LAB**

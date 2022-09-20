# Practice Lab: Administering Windows Client Using Remote Management

## Summary

In this lab you perform remote Windows administration using Remote PowerShell, Remote Desktop, and Windows Admin Center.

## Exercise 1: Administering Windows using Remote PowerShell and Remote Desktop

### Scenario

Contoso is planning to open a new branch office. To manage the devices in the new branch office you need to use Remote PowerShell and Remote Desktop. You need to test remote administration by running remote PowerShell commands on SEA-SVR2 and you need to enable Remote Desktop on SEA-CL1.

### Task 1: Perform remote management using Windows PowerShell

1. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password: **Pa55w.rd**.

2. Select **Start**, and then type **PowerShell**.

3. Under the Windows PowerShell app, select **Run as Administrator**.

4. To view all of the services that are stopped on SEA-SVR2, in the Windows PowerShell window, type the following command, and then press **Enter**:

```
Get-Service -ComputerName SEA-SVR2 | Where-Object {$_.Status -eq "Stopped"}
```

4. To view the the content of the C:\\Program Files folder on SEA-SVR2, in the Windows PowerShell window, type the following command, and then press **Enter**:

```
Invoke-Command -ComputerName SEA-SVR2 -ScriptBlock {Get-ChildItem "C:\Program Files"}
```

5. To view the the System event log on SEA-SVR2, in the Windows PowerShell window, type the following command, and then press **Enter**:

```
Invoke-Command –ComputerName SEA-SVR2 –ScriptBlock {Get-EventLog –log system}
```

6. To determine if the WinRM service is running on SEA-SVR2, in the Windows PowerShell window, type the following command, and then press **Enter**:

```
Test-WsMan SEA-SVR2
```

   *Note: The output on SEA-SVR2 validates that the WinRM service is running and it is ready to receive WS-Management requests. If it was not configured, you would have needed to run **Winrm quickconfig** on SEA-SVR2.*

7. In the Windows PowerShell window, type the following commands, and then press **Enter** after each one:

```
Enter-PSSession SEA-SVR2
Get-command
Add-Content Remote.txt "Adding text to file on SEA-SVR2"
Exit-PSSession
```

### Task 2: Enable Remote Desktop

1. On **SEA-CL1**, select **Start**, and then select the **Settings** icon.

2. On the **System** page, select **Remote Desktop**.

3. Next to **Remote Desktop** select the switch to **On** and then in the Remote Desktop Settings window select **Confirm**.

4. On the Remote Desktop page, select **Remote Desktop** to expand the available options.

5. Verify that **Require computers to use Network Level Authentication to connect** is selected. Also take note of the Current Remote Desktop Port, which is set to **3389**.

6. On the Remote Desktop page, select **Remote Desktop users**.

7. On the Remote Desktop Users page, select **Add**.

8. On the Select Users or Groups box under **Enter the object names to select (examples)** enter **Jon Cantrell** and then select **OK**.

9. Select **OK** to close the Remote Desktop Users dialog box.

10. Right-click the **Start** button and then select **Computer Management**.

11. Expand **Local Users and Groups** and then select **Groups**.

12. Double-click the **Remote Desktop Users** group.

    > Notice that Contoso\Jon is a member of the Remote Desktop Users group as configured from the Settings app. Members of this group are granted rights to sign in remotely.

13. Close all open Windows on SEA-CL1 and sign out.

14. Switch to **SEA-CL2**.

15. Sign in to SEA-CL2 as **Contoso\Jon** with the password of **Pa55w.rd**.

16. On the Start menu, enter **Remote Desktop Connection** and then select Open.

17. On the Remote Desktop Connection app, select **Show Options** to expand additional settings.

18. in the logon settings section enter the following information and then select **Connect**:

    - Computer: **SEA-CL1**
    - User name: **Contoso\Jon**

19. At the Windows Security prompt, enter the password of **Pa55w.rd** and then select **OK**. 

    > Jon signs into SEA-CL1 in full screen mode.

20. In the SEA-CL1 remote desktop window, select **Start**, select the **Power** button, and then select **Disconnect**.

21. Sign out of SEA-CL2.

**Results**: After completing this exercise, you will have enabled and tested remote PowerShell and Remote Desktop.

## Exercise 2: Administering Windows using Windows Admin Center

### Scenario

You need to test remote administration capabilities of the Windows Admin Center. For this scenario, you install Windows Admin Center on SEA-CL1 and then perform remote administration tasks on SEA-SVR1.

### Task 1: Install Windows Admin Center

1. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password: **Pa55w.rd**.

2. On the taskbar, select **File Explorer**.

3. In File Explorer, browse to **D:\\Labfiles\\Tools**, and then double-click **WindowsAdminCenter2110.msi**. Windows Installer begins the installation process.

4. On the **Windows Admin Center Setup** license page, select the check box next to **I accept these terms**, and then select **Next**.

5. On the **Send diagnostic data to Microsoft** page, select **Next**.

6. Select **I don't want to use Microsoft Update**, and then select **Next**.

7. On the **Install Windows Admin Center on Windows 10** page, select **Next**.

8. On the **Installing Windows Admin Center** page, configure the following and then select **Install**:
    - Select a port for the Windows Admin Center site: **6516**
    - Allow Windows Admin Center to modify this machine's trusted hosts settings: **Selected**
    - Create a desktop shortcut to launch Windows Admin Center: **Selected**.
    - Automatically update Windows Admin Center: **Not selected**

9. On the **One more thing** page, take note of the message and then select **Finish**.

10. Close File Explorer.

### Task 2: Add connections to Windows Admin Center

1. On **SEA-CL1**, on the desktop, double-click the **Windows Admin Center** icon.

2. In the **Select a certificate for authentication** window, select the **Windows Admin Center Client** certificate, and then select **OK**.

3. Close the **Read what's new** page.

   > Note that you receive notifications on extensions being updated. When the extension update is complete, select **OK** at the **Successfully updated your extensions** message.

4. On the **All connections** page, select **Add**.

5. On the **Add or create resources** page, in the **Servers** pane, select **Add**.

6. On the **Add one** tab, under **Server name**, type **SEA-SVR1**. Windows Admin Center queries Active Directory and then displays the server.

7. Select **Add** to add SEA-SVR1.Contoso.com to the All connections page.

### Task 3: Perform Remote Administration using Windows Admin Center

1. In the **Windows Admin Center**, select **SEA-SVR1.Contoso.com**.

2. On the **Overview** page, take note of the server information and performance statistics.

3. On the **Tools** pane, select **Events**.

4. On the **Events** pane, take note of the event logs that are available from SEA-SVR1 and then under **Windows Logs** select **System**.

5. Review the System log events and then select the **Clear** button.

6. On the **Clear** prompt, select **Clear log**.

7. On the **Tools** pane, select **Files & file sharing**.

8. In the details pane, on the **Files** tab, take note of the file structure from SEA-SVR1.

9. In the details pane, select the **File shares** tab. Take note of the current shared folders.

10. On the **Tools** pane, select **Local users & groups**. Take note of the Users and Groups tabs where you can manage local users and groups on SEA-SVR1.

11. On the **Tools** pane, select **PowerShell**. A remote PowerShell session is established to SEA-SVR1.

12. In the PowerShell pane, type `Get-Service` and then press **Enter**. SEA-SVR1 services are displayed.

13. On the **Tools** pane, select **Remote Desktop**. On the **Navigating away closes PowerShell** box, select **Continue**.

14. On the **Remote Desktop** page, read the message and then select **Go to settings**.

15. On the **Settings** page, select **Remote Desktop** and then under **Remote Desktop** select **Allow remote connections to this computer**. Select **Save**.

16. On the **Tools** pane, select **Remote Desktop**.

17. On the **Navigating away closes PowerShell** message, select **Continue**.

18. On the **Welcome to Remote Desktop** page, enter **Contoso\Administrator** as the Username with the Password of **Pa55w.rd**. 

19. Select the check box next to **Automatically connect with the certificate presented by this machine**, select **Confirm**, and then select **Connect**. The SEA-SVR1 desktop displays in the Remote Desktop pane.

20. Select **Disconnect**.

21. On the **Tools** pane, select **Roles & features**. Notice that you can remotely install or uninstall server roles and features on SEA-SVR1.

22. Close Windows Admin center and then sign out of SEA-CL1.

**Results**: After completing this exercise, you will have installed Windows Admin Center on SEA-CL1 and then performed remote administration tasks on SEA-SVR1.

**END OF LAB**

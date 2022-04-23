# Practice Lab: Installing Apps in Windows Client

## Summary

In this lab you will learn how install and update Microsoft Store Apps and how to discover and install packaged apps by using Windows Package Manager.

## Exercise 1: Installing and updating Microsoft Store apps

### Scenario

You need to test the download and update functionality of the Microsoft App Store. You will download and install an app named the **Microsoft Remote Desktop**. You also need to validate how Microsoft Store apps are updated and uninstalled.

### Lab preparation

*Note: In some situations, the Windows Update service may be disabled. Use the following steps to validate and enable the Windows update service if needed. This is not necessary to run in typical Windows client scenarios.*

1. Sign in to **SEA-WS1** as **.\Admin** with the password of **Pa55w.rd**.

2. Right-click **Start**, and then select **Windows PowerShell (Admin)**.

3. In the **User Account Control** dialog box, select **Yes**.

4. In the **Administrator: Windows PowerShell** window, type **the following
    command** and then press **Enter**.

```
Set-Service wuauserv -Startuptype Manual
```

5. Sign out of SEA-WS1.

### Task 1: Connect your Microsoft account to SEA-WS1 and SEA-WS2

> Note: You only need to complete this task if you did not complete lab **0704: Synchronizing Files with OneDrive**, or if you ended or reverted the virtual environment after lab 0704. To complete this task, you need to have a Microsoft account. You can obtain a free Microsoft account which can be created at <https://outlook.live.com>. Your instructor can guide you on how to create an account if required.

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

### Task 2: Configure app updates and uninstall an app

1. Sign in to **SEA-WS1** with your Microsoft account and the PIN **1029**.

2. Click **Start**, and then select **Microsoft Store**.

3. In the **Microsoft Store** app, select the sign in icon on the menu bar, and then select **App Settings**.

4. Next to **App updates**, verify that **Update apps automatically** is set to enabled.

5. In the **Microsoft Store** app, select the **Library** icon on the menu bar. Notice that there are several apps waiting to be updated.

6. Select **Update all**. All of the installed apps begin to download and install app updates as needed. 

7. Select **Start**, right-click **Tips**, and then select **Uninstall**.

8. In the **This app and its related information will be removed** message box, select **Uninstall**.

### Task 3: Install a Microsoft Store app

1. In the Microsoft Store app, select **Search**, type **Microsoft Remote Desktop**, and then press Enter.

2. On the **Microsoft Remote Desktop** search results, select **Get**. 

3. Close the Microsoft Store app.

4. Select **Start** and verify that Microsoft Remote Desktop is added to the Start page. It may take a while for the app to download and install. Continue with the next exercise and check back later.

**Results**: After completing this exercise, you will have managed Microsoft Store app updates, uninstalled an app, and installed a Microsoft Store app, 

## Exercise 2: Installing an app by using Windows Package Manager

### Scenario

You have been asked to install an application by using the Windows Package Manager **winget** command-line tool built into Windows 11. You will search for and install an application named **PowerToys**.

### Task 1: Search for and install an app using winget

1. On **SEA-WS1**, select **Start** and then type **PowerShell**.

2. Under Windows PowerShell, select **Run as administrator**. At the User Account Control message, select **Yes**.

3. To review the commands available with winget, type the following command and then press Enter:

    ```
    winget
    ```

4. To display a list of applications installed on the device, type the following command and then press Enter:

    ```
    winget list
    ```

    At the message prompt, type **Yes** and then press Enter.

5. To search for an available app to install from published online repositories, type the following comment and press Enter:

    ```
    winget search
    ```

6. To filter the search list, provide a search string. For example, to find all apps that have the word **Reader** associated with it, type the following command and press Enter:

    ```
    winget search reader
    ```

7. To search for the **PowerToys** app, type the following command and press Enter:

    ```
    winget search powertoys
    ```

    Notice that information is returned with the name, ID, version, and source of the package.

8. To install an app using winget, type the following command and press Enter:

    ```
    winget install --id Microsoft.Powertoys
    ```

    PowerToys downloads and installs on the local device.

9. After PowerToys installs and opens, close the **Welcome to PowerToys** window.

10. To search for additional information about the **PowerToys** app, type the following command and press Enter:

    ```
    winget show --id Microsoft.Powertoys
    ```

    Notice that detailed information is returned for the PowerToys package.

11. To uninstall an app by using winget, type the following command and press Enter:

     ```
     winget uninstall --id Microsoft.Powertoys 
     ```

12. Close PowerShell and sign out of SEA-WS1.

**Results**: After completing this exercise, you will have used the Windows Package Manager **winget** command-line tool to list and search for packaged apps. You then installed and uninstalled the PowerToys app by using the winget command-line tool. 

**END OF LAB**

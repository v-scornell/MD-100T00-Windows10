# Practice Lab: Provision a Kiosk using Configuration Designer

## Summary

In this lab, you create a provisioning package to configure a Windows 11 device to run a single application when a specific user account is used to sign in.

### Scenario

In the reception area at Contoso, it’s necessary to deploy a new Windows 11 computer as a kiosk device. This new device will only run Microsoft News to provide guests the ability to review the latest News events. You need to use the Configuration Designer to create a provisioning package to configure kiosk settings on the device.

### Prerequisites

To following lab(s) must be completed before this lab:

- 0101-Deploying Windows Desktop settings using a provisioning package - Install the Configuration Designer from the Windows Assessment and Deployment Kit.

### Task 1: Create a provisioning package

1. Sign in to **SEA-SVR2** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. On SEA-SVR2, select **Start**, expand **Windows Kits**, and then select **Windows Imaging and Configuration Designer**. 

   > The **Windows Configuration Designer** opens at the **Start page**.

3. On the **Start page**, select **Provision kiosk devices**. The **New project** window opens.

4. In the **New project** window, under **Name**, type **Kiosk Provision Package**.

5. Under **Description**, type the following:
   - Assigns a device name in the format of Kiosk-%RAND:2%. Joins the device to Contoso.com. Configures the device to run as a Kiosk.

6. Select **Finish**. A new page named **Kiosk Provision Package** displays with several configuration steps.

7. On the **Set up Device** step, configure the following setting:
   - Under **Device name**, type **Kiosk-%RAND:2%**.

8. On the **Set up network** step, select the switch to disable this step. 

   > The lab environment does not have Wi-Fi capable virtual machines and will be disabled for this scenario.

9. On the **Account management** step, configure the following settings:
   - Enroll into Active Directory: **Selected**
   - Domain name: **Contoso.com**
   - User name: **Contoso\Administrator**
   - User password: **Pa55w.rd**

10. On the **Configure kisok account and app** step, configure the following settings:

- User name: **KioskUser**
- Password: **Pa55w.rd**
- Under **Configure the kiosk mode app**, in the User name box: **KioskUser**
- App type: **Universal Windows App**
- Enter the AUMID for the app: **Microsoft.BingNews_8wekyb3d8bbwe!AppexNews** 

     > Note: you can determine the AUMID by running the **get-startapps -Name Microsoft News** PowerShell command

11. On the **Configure kisok common settings** step, review the settings, but do not change anything.

12. Select the **Finish** step and review the **Summary** information.

13. On the **Summary** page, select **Create**. Take note of the name and saved location of the package which should be:

-  Name: **Kiosk Provision Package.ppkg** 
- Saved location: **C:\\Users\\Administrator.CONTOSO\\Document\\Windows Imaging and Configuration Designer (WCID)\\Kiosk Provision Package**

14. Close the Windows Configuration Designer.

### Task 2: Deploy a provisioning package to a Windows device

1. On SEA-SVR2, on the taskbar, select **File Explorer**.

2. In **File Explorer**, under **Quick access**, select **Documents**.

3. In the **Documents** folder, open the **Windows Imaging and Configuration Designer (WCID)** folder.

4. From the **Windows Imaging and Configuration Designer (WCID)** folder, select the **Kiosk Provision Package** folder.

5. On the **Home** tab, select **Copy** .

6. In the navigation pane, select **Allfiles (E:)**.

7. Open the **Labfiles** folder and then open the **Provisioning** folder.

8. On the **Home** tab, select **Paste** to copy the **Kiosk Provision Package**  folder to the **Provisioning** folder.

9. Close **File Explorer**.

10. Switch to **SEA-WS2** and sign in as **Admin** with the password of **Pa55w.rd**.

11. On the taskbar, select **File Explorer**.

12. In the address bar, type **\\\\SEA-SVR2\\Labfiles** and then press Enter.

13. When prompted, in the **Windows Security** box, enter **Contoso\Administrator** with the password of **Pa55w.rd**.

14. Open the **Provisioning** folder.

15. Select the **Kiosk Provision Package** folder, and then select **Copy**.

16. In the navigation pane, select **Downloads**, and then select **Paste** to copy the **Kiosk Provision Package** folder to the **Downloads** folder.

17. From the **Downloads** folder, open the **Kiosk Provision Package** folder and then run the **Kiosk Provision Package.ppkg** file.

18. At the **User Account Control** box, select **Yes**. A dialog box opens that states **Is this package from a source you trust?** 

19. Read the package details and then select **Yes, add it**.

    > In a few moments, a message displays that states that Windows will shut down in 1 minute. 

20. Select **Close** and then wait until the device restarts.

### Task 3: Validate the configuration

1. After the device restarts, select **Other user** and sign in as **.\\KioskUser** with the password of **Pa55w.rd**. 

   > Wait for the initial profile to be configured. After a moment, you are signed in. This verifies that the local account, KioskUser, was created. Microsoft News opens. This verifies that the kiosk application was assigned.

2. To enter administrative mode for the Kiosk, press **Ctrl+Alt+Delete**, select **Other user,** and sign in as **Contoso\Administrator** with the password of **Pa55w.rd**.

   > Wait for the initial profile to be configured. After a moment, you are signed in. Note that the kiosk mode is only active when KioskUser is signed in. The Contoso\Administrator account signs in to the standard Windows 11 desktop.

**Results**: After finishing this lab, you will have successfully deployed a provisioning package to configure a Windows 11 device as a kiosk to run a single application when a specific user account is used to sign in.

**END OF LAB**

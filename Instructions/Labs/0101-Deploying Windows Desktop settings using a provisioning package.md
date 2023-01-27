# Practice Lab: Deploying Windows Desktop settings using a provisioning package

## Summary

In this lab, you identify the tools included in the Windows ADK, install the Configuration Designer component of the Windows ADK, create a provisioning package, and then deploy the configuration package to a Windows 11 desktop device.

### Scenario

As part of the Desktop Administration team at Contoso, you have been tasked with deploying new Windows 11 desktop devices to users. The devices have been purchased with Windows 11 pre-installed. You need to use the Configuration Designer to create a provisioning package that applies the following settings on the new devices:

- A device name in the format of **SEA-CL%RAND:2%**, which specifies SEA-CL with two random numbers.
- Join the device to the Contoso.com Active Directory domain.
- Create a local administrator account with the name LocalAdmin with the password of Pa55w.rd.
- Install two applications named PowerToys and  Power BI Desktop to the device.

### Task 1: Identify the Windows ADK tools

1. Sign in to **SEA-SVR2** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. On the taskbar, select **Start** and then select **Control Panel**.

3. Select **Programs**, and then select **Programs and Features**. 

    > Notice that the **Windows Assessment and Deployment Kit** and the **Windows Assessment and Deployment Kit Windows Preinstallation Environment Add-ons** programs are installed.

4. Select **Windows Assessment and Deployment Kit** and then select **Change**.

5. On the **Maintain your Windows Assessment and Deployment Kit features** page, ensure that **Change** is selected and then select **Next**.

6. Notice the features that have been installed on SEA-SVR2. Features include:
    - Deployment Tools

    - User State Migration Tool (USMT)

    - Microsoft User Experience Virtualization (UE-V) Template

      > Notice that Configuration Designer is not installed.

7. Select the check box next to **Configuration Designer**, and then select **Change**.

8. On the Windows Assessment and Deployment Kit window, select **Close**.

9. Close the **Programs and Features** window.

### Task 2: Create a provisioning package

1. On SEA-SVR2, select **Start**, expand **Windows Kits**, and then select **Windows Imaging and Configuration Designer**. 

   > The **Windows Configuration Designer** opens at the **Start page**.

2. On the **Start page**, select **Provision desktop devices**. The **New project** window opens.

3. In the **New project** window, under **Name**, type **Windows 11 Provision Package**.

4. Under **Description**, type the following:
   - Assigns a device name in the format of SEA-CL%RAND:2%. Joins the device to Contoso.com. Creates a local administrator account with the name LocalAdmin with the password of Pa55w.rd, and adds an application named PowerToys to the device.

5. Select **Finish**. A new page named **Windows 11 Provision Package** displays with several configuration steps.

6. On the **Set up Device** step, configure the following setting:
   - Under **Device name**, type **SEA-CL%RAND:2%**.

7. On the **Set up network** step, under **Set up network**, disable the **Connect devices to a Wi-Fi network** option. 

   > The lab environment does not have Wi-Fi capable virtual machines and will be disabled for this scenario.

8. On the **Account management** step, configure the following settings:
   - Enroll into Active Directory: **Selected**
   - Domain name: **Contoso.com**
   - User name: **Contoso\Administrator**
   - User password: **Pa55w.rd**
   - Under Optional: Create a local administrator account enter **LocalAdmin** as the User name and **Pa55w.rd** as the Password.

9. On the **Add applications** step, select **Add an application** and then configure the following settings:
   - Application name: **Power BI Desktop**
   - Installer path: **E:\\Labfiles\\Apps\\PowerBI\\PBIDesktop_x64.msi**
   - Continue installations after failure: **Yes**
   - In the **Command line arguments** box, at the end of the command add **ACCEPT_EULA=1** and then select **Add**.

10. On the **Add applications** step, select **Add an application** and then configure the following settings:
    - Application name: **PowerToys**
    - Installer path: **E:\\Labfiles\\Apps\\PowerToys\\PowerToysSetup-x64.exe**
    - In the **Command line arguments** box, at the end of the command add **-passive** and then select **Add**. The passive switch allows the display of the installation status, but will not require any input.

11. Select the **Finish** step and review the **Summary** information.

12. On the **Summary** page, select **Create**. Take note of the name and saved location of the package which should be:
    -  Name: **Windows 11 Provision Package.ppkg** 
    - Saved location: **C:\\Users\\Administrator.CONTOSO\\Document\\Windows Imaging and Configuration Designer (WCID)\\Windows 11 Provision Package**

13. Close the Windows Configuration Designer.

### Task 3: Deploy a provisioning package to a Windows device

1. On SEA-SVR2, on the taskbar, select **File Explorer**.

2. In **File Explorer**, under **Quick access**, select **Documents**.

3. In the **Documents** folder, open the **Windows Imaging and Configuration Designer (WCID)** folder.

4. From the **Windows Imaging and Configuration Designer (WCID)** folder, select the **Windows 11 Provision Package** folder.

5. On the **Home** tab, select **Copy** .

6. In the navigation pane, select **Allfiles (E:)**.

7. Open the **Labfiles** folder and then open the **Provisioning** folder.

8. On the **Home** tab, select **Paste** to copy the **Windows 11 Provision Package**  folder to the **Provisioning** folder.

9. Close **File Explorer**.

10. Switch to **SEA-WS1** and sign in as **Admin** with the password of **Pa55w.rd**.

11. On the taskbar, select **File Explorer**.

12. In the address bar, type **\\\\SEA-SVR2\\Labfiles** and then press Enter.

13. When prompted, in the **Windows Security** box, enter **Contoso\Administrator** with the password of **Pa55w.rd**.

14. Open the **Provisioning** folder.

15. Select the **Windows 11 Provision Package** folder, and then select **Copy**.

16. In the navigation pane, select **Downloads**, and then select **Paste** the **Windows 11 Provision Package** folder to the **Downloads** folder.

17. From the **Downloads** folder, open the **Windows 11 Provision Package** folder and then run the **Windows 11 Provision Package.ppkg** file.

18. At the **User Account Control** box, select **Yes**. A dialog box opens that states **Is this package from a source you trust?** 

19. Read the package details and then select **Yes, add it**.

    > In a couple of minutes, the two apps install, followed by a message that Windows will shut down in 1 minute. 

20. Select **Close** and then wait until the device restarts.

### Task 4: Validate the configuration

1. After the device restarts, select **Other user** and sign in as **Contoso\\Jon** with the password of **Pa55w.rd**. Wait for the initial profile to be configured.

2. On the Start menu, select **Settings**.

3. On the **System** page, verify that the Computer name is **SEA-CL** followed by two random numbers.

4. On the Start menu, select **Apps** and then select **Apps & features**.

5. Verify that both **Microsoft Power BI Desktop (x64)** and **PowerToys (Preview) x64** are both listed as installed applications.

6. Close the **Settings** window.

7. Right-click the Start button, and then select **Computer Management**.

8. In Computer Management, expand **Local Users and Groups**, and then select **Users**. 

9. Verify that the **LocalAdmin** user account is configured on the device.

10. Close Computer Management and then sign out of the computer.

**Results**: After finishing this lab, you will have successfully used Configuration Designer to create a provisioning package. You have also deployed the provisioning package to a Windows 11 device and verifed the changes.

**END OF LAB**

# Practice Lab: Managing Windows Update Settings

## Summary

In this lab you manage Windows Update settings for a single device and configure feature and quality update settings for multiple devices using Windows Update for Business Group Policy settings.

## Exercise 1: Configuring Windows Update for a Single Device

### Scenario

You need to validate the Windows Update settings for SEA-WS3. You have also been asked to ensure that the following Windows update settings are applied to the device:

- Updates for other Microsoft products should be enabled.
- A notification must be shown when the device requires a restart to finish updating.
- Delivery optimization must be configured to allow downloads from the internet and the local network.
- Active hours should be configured to be 7:00 AM to 8:00 PM.
- Updates should be paused for 2 weeks.

### Task 1: Configure Windows Update

1. Sign in to **SEA-WS3** as **.\Admin** with the Password of **Pa55w.rd**

2. Select **Start**, and then enter **PowerShell**.

3. In the Search results, under Windows PowerShell, select **Run as administrator**. In the User Account Control dialog box, select **Yes**.

4. In the Administrator: Windows PowerShell window, type the following command, and then press Enter:

```
Set-Service wuauserv -StartupType Manual
```

_Note: For the lab setup, the Windows Update service is disabled. The above command is not necessary to run in typical Windows 10 scenarios._

5. Close Windows PowerShell.

6. Select **Start**, and then select the **Settings** icon.

7. In **Settings**, select **Windows Update**.

8. On the **Windows Update** tab, select **Advanced options**.

9. On the **Advanced options** page, enable the **Receive updates for other Microsoft products **option.

10. On the **Advanced options** page, enable the **Notify me when a restart is required to finish updating** option.

11. Scroll down and then select **Delivery Optimization**.

12. On the Delivery Optimization page, verify that the **Allow downloads from other PCs** option is enabled.

13. Select **Devices on the internet and my local network**.

14. Scroll down and then select **Activity monitor**. Take note of the Download Statistics and Upload Statistics and then select the **Delivery Optimization** link.

15. In the navigation pane, select **Windows Update**.

### Task 2: Change active hours, review applied updates, and pause updates

1. On the **Windows Update** page, select **Advanced options**.

2. On the **Advanced options** page, select **Active hours**.

   > Verify that the current active hours are from 8:00AM to 5:00PM. 

3. Next to Adjust active hours, select **Manually** and then change the **Start time to 7:00AM** and the **End time to 8:00PM**.

4. In the navigation pane, select **Windows Update**.

5. On the **Windows Update** page, select **Update history**.

6. Review the updates listed, and then select **Uninstall updates**.

7. Review the updates listed in **Installed Updates**. Close **Installed Updates**.

8. In the navigation pane, select **Windows Update**.

9. Next to **Pause updates**, select the drop-down menu and select **Pause for 2 weeks**.

   > Notice that the Windows Update indicator displays that updates are paused. You can also select **Resume updates** if needed.

10. Close the **Settings** page.

11. Sign out of SEA-WS3.

**Results**: After completing this exercise, you will have successfully validated and configured Windows Update settings.

## Exercise 2: Managing Feature and Quality Updates with Windows Update for Business

### Scenario

Contoso uses Windows Update for Business to manage the updates for Windows 10 devices.

You have been delegated the task to create Group Policy Objects to configure Windows Update for Business for your Windows 10 devices. Your first task is to determine how many deployment rings you will need and the associated Windows update settings based upon business requirements. You then need to configure a Group Policy object for each deployment ring. The Group Policy Objects will then be linked to organizational units by the Active Directory administrators at a later time.

### Task 1: Identify Windows Update for Business Requirements

Contoso currently configures each Windows 10 device to apply Windows updates based upon manual operating system settings. However a number of issues have come up that requires you to revisit and propose a new solution:

- Updates are not fully tested before they are installed on the all the computers in the organization. This is especially troublesome for when a new feature update is released.
- Some users have been pausing updates for an extended period of time.
- Some users have been enrolling into the Windows Insider Program, which has caused compatibility issues for some of the devices.
- It is difficult to maintain and manage the Windows 10 update settings using the current manual process.

You have been asked to address these issues by:

- Ensuring that updates are tested at least 10 days before being deployed to everyone in the organization.
- Restricting standard users from configuring Windows Update settings.
- Implementing Windows Update for Business.

You need to develop a plan to implement Windows Update for Business. Consider the following questions to help you with your solution:

1. How will you ensure that an update has been tested properly before being deployed throughout the entire organization? *Answer: Create Active Directory Group Policy Objects that align with deployment rings. One possible solution is to create a pilot deployment ring that does not defer quality or feature updates. This will allow any device that has this policy to immediately obtain a released update and start its testing process. A second Broad deployment ring can be created that has a deferral for 10 days for both quality and feature updates. This second object would be applied to the rest of the organization and will not receive released updates until 10 days have passed.*
2. How will you ensure that standard users are restricted from configuring Windows Updates? *Answer: Using Group Policy settings will provide the ability to restrict various settings such as pausing updates and enrolling into the Windows Insiders Program.*
3. How will you manage and maintain Windows Updates for your organization? *Answer: Windows Update for Business uses Active Directory Group Policy. For more granular control and management, Microsoft Intune or Microsoft Endpoint Configuration Manager can also be used.*

### Task 2: Use Group Policy to configure Windows Update for Business  

1. Sign in to SEA-SVR1 as **Contoso\\Administrator** with the password of **Pa55w.rd**.

2. In Server Manager, select **Tools** and then select **Group Policy Management**.

3. Maximize the Group Policy Management window. In the console tree, expand **Forest:Contoso.com**, expand **Domains**, and then expand **Contoso.com**. Select the **Group Policy Objects** node.

4. Right-click the **Group Policy Objects** node, and then select **New**.

5. In the **New GPO** dialog box, in the **Name** box, type **Pilot Release - Ring 1**, and then select **OK**.

6. In the details pane, right-click **Pilot Release - Ring 1**, and then select **Edit**. Maximize the Group Policy Management Editor window.

7. In the console tree, under **Computer Configuration**, expand **Policies**, expand **Administrative Templates**, expand **Windows Components**, and then select **Windows Update**.

8. In the details pane, double-click **Configure Automatic Updates**.

10. In the **Automatic Updates** window, configure the following and then select **OK**:
     - Enabled: **Selected**
     - Configure automatic updating: **4 - Auto download and schedule the install**
     - Install updates for other Microsoft products: **Selected**

11. In the details pane, double-click **Windows Update for Business**.

12. In the details pane, double-click **Manage preview builds**.

13. In the **Manage preview builds** window, select **Disabled**, and then select **OK**.

14. In the details pane, double-click **Select when Preview Builds and Feature Updates are received**.

15. In the **Select when Preview Builds and Feature Updates are received** window, configure the following and then select **OK**:

- Enabled: **Selected**
 How many days after a Feature Update is released would you like to defer the update before it is offered to the device?: **0**

> The Pilot Release - Ring 1 configuration will not have any updates deferred.

16. In the details pane, double-click **Select when Quality Updates are received**.

17. In the **Select when Quality Updates are received** window, configure the following and then select **OK**:
     - Enabled: **Selected**
     - After a quality update is released, defer receiving it for this many days: **0**

### Task 3: Use Group Policy to configure Windows Update experience for users  

1. On SEA-SVR1, ensure that you are still in the Group Policy Management Editor for the **Pilot Release - Ring 1** policy.

2. In the console tree, under **Computer Configuration**, expand **Policies**, expand **Administrative Templates**, expand **Windows Components**, and then select **Windows Update**.

3. In the details pane, double-click **Remove access to "Pause updates" feature**.

4. In the **Remove access to "Pause updates" feature** window, select **Enabled** and then select **OK**.

5. In the details pane, double-click **Specify deadline before auto-restart for update installation**.

6. In the **Specify deadline before auto-restart for update installation** window, configure the following and then select **OK**:
    - Enabled: **Selected**
    - Specify the number of days before a pending restart will automatically be executed outside of active hours: Quality Updates (days): **3**; Feature Updates (days): **3**

7. Close the Group Policy Management Editor.

### Task 4: Use Group Policy to configure the Broad Release update ring  

1. On SEA-SVR1, ensure that you are still in the Group Policy Management console.

2. Maximize the Group Policy Management window. In the console tree, expand **Forest:Contoso.com**, expand **Domains**, and then expand **Contoso.com**. Select the **Group Policy Objects** node.

3. In the details pane, right-click **Pilot Release - Ring 1**, and then select **Copy**.

4. Right-click the **Group Policy Objects** node and then select **Paste**.

5. In the **Copy GPO** dialog box, ensure that **Use the default permissions for new GPOs** is selected and then select **OK**.

6. At the **Copy** dialog box, select **OK**.

7. In the details pane, select **Copy of Pilot Release - Ring 1** and then select **Rename**. Rename the object to **Broad Release - Ring 2**.

8. Right-click **Broad Release - Ring 2** and then select **Edit**.

9. In the console tree, under **Computer Configuration**, expand **Policies**, expand **Administrative Templates**, expand **Windows Components**, and then select **Windows Update**.

10. In the details pane, double-click **Windows Update for Business**.

11. In the details pane, double-click **Select when Preview Builds and Feature Updates are received**.

12. In the **Select when Preview Builds and Feature Updates are received** window, configure the following and then select **OK**:
     - Enabled: **Selected**
     - How many days after a Feature Update is released would you like to defer the update before it is offered to the device?: **10**

13. In the details pane, double-click **Select when Quality Updates are received**.
14. In the **Select when Quality Updates are received** window, configure the following and then select **OK**:
     - Enabled: **Selected**
     - After a quality update is released, defer receiving it for this many days: **10**

15. Close the Group Policy Management Editor.

16. Close the Group Policy Management console.

17. Sign out of SEA-SVR1.

**Results**: After completing this exercise, you will have successfully configured Group Policy Objects to be later assigned to organizational units to manage Windows Update for Business settings.

**END OF LAB**

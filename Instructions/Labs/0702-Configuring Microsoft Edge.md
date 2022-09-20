# Practice Lab: Configuring Microsoft Edge

## Summary

In this lab you will learn how to configure the Internet Explorer Enterprise Mode to provide compatibility for Microsoft Edge to open legacy web sites.

### Prerequisites

To following lab(s) must be completed before this lab:

- 0402-Configuring and Testing Name Resolution - Exercise 2: Testing Name Resolution

## Exercise 1: Configuring Microsoft Edge to support Internet Explorer Enterprise Mode

### Scenario

Contoso uses a web site located at intranet.contoso.com. This site currently only works properly using older Internet Explorer versions. As you recently upgraded all devices to the latest version of Microsoft Edge Chromium, you must ensure that this web site still opens and works with compatibility mode.

_Note: This Exercise requires that a DNS CNAME entry for intranet.Contoso.com be added which resolves to SEA-CFG1.Contoso.com. This task is performed in Module 5 lab 0502-Configuring and Testing Name Resolution. Also note that Microsoft Edge .admx templates have already been installed to allow for the creation of Microsoft Edge Chromium group policy settings._

### Task 1: Verify the site is not displayed in Enterprise Mode

1. Sign in to **SEA-CL1** as **Contoso\\Cari** with the password **Pa55w.rd**.

2. On the task bar, select **Microsoft Edge**.

3. In the Microsoft Edge window, select **Start without your data**, and then select **Confirm and start browsing**.

4. Close Microsoft Edge.

5. On the task bar, select **Microsoft Edge**

6. In the Microsoft Edge Address bar, type **edge://compat/enterprise**, and then press **Enter**. Notice that the Enterprise Mode Site List does not contain any entries.

7. Sign out of **SEA-CL1**.

### Task 2: Create a Site list for Internet Explorer Enterprise Mode

1. Switch to **SEA-CFG1**.

2. Sign in to **SEA-CFG1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

3. Select the **File Explorer** icon on the taskbar.

4. In File Explorer, browse to **\\\\SEA-DC1\\Labfiles\\Apps**.

5. Double-click the **EMIESiteListManager.msi** file.

6. In the Enterprise Mode Site List Manager Setup window, select **Next**.

7. On the End-User License Agreement page, select the check box for **I accept the terms in the License Agreement**, and then select **Next**.

8. On the Destination Folder page, select **Next**.

9. On the Ready to install Enterprise Mode Site List Manager page, select **Install**.

10. On the Completed the Enterprise Mode Site List Manager Setup Wizard page, select **Finish**.

11. Close File Explorer.

12. Select the **Start** button, type **Enterprise**, right-click **Enterprise Mode Site List Manager** and select **Run as administrator**.

13. In the Enterprise Mode Site List Manager for v.2 schema window, select **Add**.

14. In the Add new website window, in the URL text box, type **intranet.contoso.com**. In the Compat Mode drop-down list box, select **IE9 Document Mode**, and then select **Save**.

15. Select the **File** menu, and then select **Save to XML**.

16. In the Save as… dialog box, navigate to **C:\\inetpub\\wwwroot**. In the File name text box, type **ContosoEnterpriseMode**, and then select **Save**.

17. Close Enterprise Mode Site List Manager.

18. On the task bar, select **Microsoft Edge**.

19. In the Address bar, type **<http://Intranet.Contoso.com/ContosoEnterpriseMode.xml>**, and then press **Enter**.

20. Verify that the XML file opens correctly.

21. Close **Microsoft Edge**.

### Task 3: Create a policy to enable Internet Explorer Enterprise Mode  

1. Switch to SEA-SVR1.

2. Sign in to **SEA-SVR1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

3. On SEA-SVR1, switch to **Server Manager**, select **Tools**, and then select **Group Policy Management**.

4. In the Group Policy Management window, expand **Forest: Contoso.com**, expand **Domains**, expand **Contoso.com**, and select **Group Policy Objects**.

5. Right-click **Group Policy Objects**, and then select **New**.

6. In the New GPO dialog box, in the Name box, type **Internet Explorer Enterprise Mode Policy**,
    and then select **OK**.

7. Right-click **Internet Explorer Enterprise Mode Policy**, and then select **Edit**.

8. In the Group Policy Management Editor window, in the left pane, expand **Computer Configuration**, expand **Policies**, expand **Administrative Templates**, and then select **Microsoft Edge**.

9. In the content pane, double-click **Configure Internet Explorer integration**.

10. Select **Enabled**, and then from the **Configure Internet Explorer integration** drop down menu, select **Internet Explorer mode** and then select **OK**.

11. In the content pane, double-click **Configure the Enterprise Mode Site List**. (Be careful NOT to choose Configure the Enterprise Mode Cloud Site List.)

12. Select **Enabled**, in the **Configure the Enterprise Mode Site List** text box, type **<http://Intranet.Contoso.com/ContosoEnterpriseMode.xml>**, and then select **OK**.

13. Close the Group Policy Management Editor window.

14. In the Group Policy Management window, right-click the **Contoso.com** domain, and then select **Link an existing GPO**.

15. In the Select GPO window, select **Internet Explorer Enterprise Mode Policy**, and select **OK**.

16. Close the Group Policy Management window.

### Task 4: Verify the site is now in enterprise mode

1. Switch to **SEA-CL1** and sign in as **Contoso\\Cari** with the password of **Pa55w.rd**.

2. Select **Start** and type **cmd**. Press **Enter**.

3. At the command prompt, type the following command, and then press Enter.

    `gpupdate /force`

4. On the task bar, select **Microsoft Edge**.

5. In the Microsoft Edge Address bar, type **edge://compat/enterprise**, and then press **Enter**. Notice that the Enterprise Mode Site List contains <http://intranet.contoso.com/ContosoEnterpriseMode.xml>. If it does not appear immediately, click **Force update**.

6. In the Microsoft Edge Address bar, type **<http://intranet.Contoso.com>**, and then press **Enter**.

7. Verify that the website displays correctly, and that the Internet Explorer mode icon appears in the address bar. Select the Internet Explorer mode icon to view information about how this site opens.

8. Sign out of **SEA-CL1**.

**Results**: After completing this exercise, you should have successfully configured the Internet Explorer Enterprise Mode for Microsoft Edge.

## Exercise 2: Configuring Microsoft Edge Synchronization

### Scenario

You frequently use two devices, SEA-WS1 and SEA-WS2, and would like to ensure that Microsoft Edge favorites are synchronized between the two devices. You need configure Microsoft Edge synchronization settings between the devices.

### Task 1: Connect your Microsoft account to SEA-WS1 and SEA-WS2

> Note: You only need to complete this task if you did not complete lab **0704: Synchronizing Files with OneDrive**, or if you ended or reverted the virtual environment after lab 0704. To complete this task, you need to have a Microsoft account. You can obtain a free Microsoft account which can be created at <https://outlook.live.com>. Your instructor can guide you on how to create an account if required.

1. Sign in to **SEA-WS1** as **Student** with the password **Pa55w.rd**.

2. Select **Start** and then select **Settings**.

3. In the **Windows Settings** page, select **Accounts**.

4. On the **Accounts** page, select **Your info**.

5. Select the link that states **Sign in with a Microsoft account instead**.

6. In the **Microsoft account Sign in** page, enter your Microsoft account email address and then select **Next**.

7. On the **Enter password** page, enter your Microsoft account password and then select **Sign in**.

8. In the **Sign into this computer using your Microsoft account** page, enter **Pa55w.rd** and then select **Next**.

10. On the **Create a PIN** page, select **Next**.

11. In the **Set up a PIN** dialog box, enter **1029** in both the **New PIN** and **Confirm PIN** boxes. Select **OK**. Notice that your Microsoft account is now listed on the Your info page.

12. Sign out of SEA-WS1.

15. Repeat steps 1-11 on SEA-WS2.

### Task 2: Configure synchronization on SEA-WS1

1. On SEA-WS1, sign in with your Microsoft account using the PIN **1029**.

2. Select **Start**, then **Settings**, then select **Accounts**.

3. Select **Windows backup**.

4. Verify that **Remember my apps** is enabled.

5. Select **Remember my preferences** and verify that all options such as **Passwords**, **Language preferences**, and **Other Windows settings** are all enabled.

6. Close **Settings**.

7. On the taskbar, select **Microsoft Edge**.

8. At the **Sync your profile** prompt, select **Sync**.

9. At the end of the address bar, select the **Settings and more** ellipse button and then select **Settings**.

10. On the **Profiles** page, select **Sync**. Take note of the Edge settings that will be automatically synced. 

11. Enable both the **History** and **Open tabs** sync settings. 

12. On the Settings pane, select **Appearance**.

13. Scroll down to the **Customize toolbar** section and then next to **Show favorites bar** select **Always**.

14. In Microsoft Edge, navigate to <http://www.microsoft.com/learn>.

15. In the address bar, select the **Add this page to favorites** button to save as a favorite.

16. Ensure that the **Folder **shows **Favorites bar**, and then select **Done**.

17. Sign out of SEA-WS1.


### Task 3: Configure synchronization on SEA-WS2

1. Sign in to **SEA-WS2** with your Microsoft account using the PIN **1029**.

2. On the taskbar, select **Microsoft Edge**.

3. At the **Sync your profile** prompt, select **Sync**. Notice that the Favorites bar and the saved favorite is available in the browser on SEA-WS2.

4. In the Microsoft Edge browser, select **Settings and more**, and then select **Settings**.

5. Select **Sync** and then validate the sync settings for Microsoft Edge.

6. Enable sync for both **History** and **Open tabs**.

7. In the address bar, enter <https://docs.microsoft.com> and press Enter.

8. In the address bar, select the **Add this page to favorites** button to save as a favorite.

9. Ensure that the **Folder** shows **Favorites bar**, and then select **Done**.

10. In the address bar. select the **Collections** button and then in the Collections pane, select **Next** to complete the introduction.

11. Under **New collection**, select **Add current page**.

12. In the **Favorites** bar, select **Microsoft Learn**, and then in the **New collection** pane, select **Add current page** to add this second page to the collection.

13. Close **Microsoft Edge**.

14. Sign out of SEA-WS2.

### Task 4: Validate synchronization

1. On SEA-WS1, sign in with your Microsoft account using the PIN **1029**.

2. On the taskbar, select **Microsoft Edge**.

3. Verify that there are two favorites attached to the Favorites bar.

4. Select the **Collections** button.

5. Select **New collection** and verify that the two pages that you added in the previous task are available in the collection. If it is not visible, create another collection and verify that the collection syncs.

6. Close **Microsoft Edge**.

7. Sign out of SEA-WS1.

**Results:** After finishing this exercise, you will have added your Microsoft account to multiple devices and configure synchronization settings between the devices.

**END OF LAB**

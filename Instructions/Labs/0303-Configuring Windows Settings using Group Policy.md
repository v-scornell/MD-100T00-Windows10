# Practice Lab: Configuring Windows Settings using Group Policy

## Summary

In this lab you will create, validate, and troubleshoot Active Directory Group Policy Objects used to configure settings on Windows clients.

## Exercise 1: Creating a Group Policy Object

### Scenario

You have been delegated the task to create Group Policy Objects for the Contoso.com domain. Your first task create a group policy object that will display a warning message to anyone signing into a Research workstation. The message will warn the user that only authorized members of the research department are permitted to sign into the workstation. You will also create a second group policy object that will place a shortcut on the Windows desktop to write.exe for all members of the Marketing department.

### Task 1: Create a Group Policy Object to configure security settings  

1. Sign in to **SEA-SVR1** as **Contoso\\Administrator** with the password of **Pa55w.rd**.

2. If necessary, select **Start**, and then select **Server Manager**.

3. Select **Tools** and then select **Group Policy Management**.

4. Maximize the Group Policy Management window. In the console tree, expand **Forest:Contoso.com**, expand **Domains**, and then expand **Contoso.com**. Select the **Group Policy Objects** node.

5. Right-click the **Group Policy Objects** node, and then select **New**.

6. In the **New GPO** dialog box, in the **Name** box, type **Security Settings Policy**, and then select **OK**.

7. In the details pane, right-click **Security Settings Policy**, and then select **Edit**. Maximize the **Group Policy Management Editor** window.

8. In the console tree, under **Computer Configuration**, expand **Policies**, expand **Windows Settings**, expand **Security Settings**, expand **Local Policies**, and then select **Security Options**.

9. In the details pane, double-click **Interactive logon: Message text for users attempting to log on**.

10. In the Interactive logon box, select the check box next to **Define this policy setting in the template** and then enter **Only members of the Research department are authorized to sign in to Research workstations**. 

11. Select **OK** to close the dialog box.

12. In the details pane, double-click **Interactive logon: Message title for users attempting to log on**.

13. In the Interactive logon box, select the check box next to **Define this policy setting** and then enter **Warning**. 

14. Select **OK** to close the dialog box.

15. Close the **Group Policy Management Editor**.

16. Double-click the **Security Settings Policy** and review the details for the group policy object. 

    > Take note that security filtering is configured to apply to all authenticated users by default.

### Task 2: Create a Group Policy Object to configure Preferences  

1. In the Group Policy Management console, right-click the **Group Policy Objects** node, and then select **New**.

2. In the **New GPO** dialog box, in the **Name** box, type **Desktop Shortcut Policy**, and then select **OK**.

3. In the details pane, right-click **Desktop Shortcut Policy**, and then select **Edit**. Maximize the **Group Policy Management Editor** window.

4. In the console tree, under **User Configuration**, expand **Preferences**, expand **Windows Settings**, and then select **Shortcuts**.

5. Right-click **Shortcuts**, point to **New**, and then select **Shortcut**.

6. In the **New Shortcut Properties** dialog box, in the **Name** box, type **Write**.

7. In the **Location** drop-down menu, select **Desktop**.

8. In the **Target path** text box, enter **C:\\Windows\\write.exe**.

9. In the **Icon file path** section, select the ellipse button and select an icon to represent the app.

10. On the **Common** tab, select the check box next to **Remove this item when it is no longer applied.** Select **OK** at the warning message.

11. Select **OK** to close the **New Shortcut Properties** box.

12. Close the **Group Policy Management Editor**.

13. Double-click the **Desktop Shortcut Policy** and review the details for the group policy object. 

    > Take note that security filtering is configured to apply to all authenticated users by default.

**Results**: After completing this exercise, you will have successfully created Group Policy Objects.

## Exercise 2: Assigning and Validating a Group Policy Object

### Scenario

You have created two group policy objects. The **Security Settings Policy** GPO must be assigned to a new Organizational Unit named **ResearchLab**. SEA-CL2 will then be moved to ResearchLab for you to test out the new policy assignment. The Desktop Shortcut Policy GPO must be assigned to members of the Marketing OU.

You need to create the additional Active Directory objects and link the GPOs. You will then validate that the GPOs apply as required.

### Task 1: Configure the Security Settings Policy GPO  

1. In the **Group Policy Management** console, right-click **Contoso.com** and then select **Active Directory Users and Computers**. 

2. In **Active Directory Users and Computers**, right-click **Contoso.com**, point to **New**, and then select **Organizational Unit**.

3. In the **New Object - Organizational Unit** box, under **Name**, type **ResearchLab** and then select **OK**.

4. Select the **Seattle Clients** OU.

5. Right-click **SEA-CL2**, and then select **Move**.

6. In the Move box, select **ResearchLab**, and then select **OK**. 

7. Select **ResearchLab** and validate that SEA-CL2 is now a member of the ResearchLab OU.

8. Minimize **Active Directory Users and Computers**.

9. Maximize the Group Policy Management window. In the console tree, expand **Forest:Contoso.com**, expand **Domains**, and then expand **Contoso.com**. Select the **Group Policy Objects** node.

10. Right-click the **ResearchLab** OU, and then select **Link an existing GPO**.

11. Select **Security Settings Policy** and then select **OK**.

### Task 2: Configure the Desktop Shortcut Policy GPO  

1. In the Group Policy Management console, right-click the **Marketing** OU, and then select **Link an existing GPO**.

2. Select **Desktop Shortcut Policy** and then select **OK**.

3. Close all open windows on SEA-SVR1.

### Task 3: Validate the Group Policy Object settings  

1. Switch to **SEA-CL2** and from the sign-in screen select the **Power** button and then select **Restart**.

2. After SEA-CL2 restarts, attempt to sign in. Notice the Warning message that displays.

3. Switch to **SEA-CL1** and sign in as **Contoso\Alice** with the password of **Pa55w.rd**.

4. On the SEA-CL1 desktop, take note of the shortcut to **Write.exe**. Alice is a member of the Marketing OU.

5. Sign out of SEA-CL1 and then sign in as **Contoso\Scott** with the password of **Pa55w.rd**.

6. On the SEA-CL1 desktop, notice that there is no shortcut. Scott is a member of the Research OU which does not have the policy applied.

7. Sign out of SEA-CL1.

8. Switch to **SEA-SVR1**.

9. Restore **Active Directory Users and Computers**. 

10. Select the **ResearchLab** OU.

11. Right-click **SEA-CL2**, and then select **Move**.

12. In the Move box, select **Seattle Clients**, and then select **OK**. 

13. Select **Seattle Clients** and validate that SEA-CL2 is now a member.

14. Switch to **SEA-CL2** and from the sign-in screen, select **OK** at the warning, select the **Power** button and then select **Restart**.

**Results**: After completing this exercise, you will have successfully assigned and validated the Group Policy Object settings.

## Exercise 3: Troubleshooting Group Policy

### Scenario

Contoso Sales Managers have requested that a shortcut to a Contacts app be placed on the desktop of their workstations. An administrator has created a Group Policy Object that applies the setting. However, Paul Koch, who is one of the Sales Managers, reports that the shortcut does not display on his workstation named SEA-CL1. You have been asked to troubleshoot the issue and ensure that the Contacts app shortcut appears for only members of the Sales Managers group.

> Note: You may want to try to address the issue on your own before completing the following tasks. The following tasks provide the steps and reveal the issues to be addressed and can be used as an answer key if needed. Hint: There are two issues you will need to fix.

### Task 1: Verify current settings  

1. Sign in to **SEA-CL1** as **Contoso\\Paul** with the password of **Pa55w.rd**. Notice that there is no shortcut to the Contacts app.

2. Select **Start**, and then enter **cmd**. Under **Command Prompt**, select **Run as administrator**.

3. At the User Account Control, enter **Administrator** with the password of **Pa55w.rd**.

4. At the command prompt type the following command and press **Enter**:

   ```
   gpresult /R
   ```

5. Review the information to validate which GPOs were applied, which GPOs were filtered, and if there are any errors reported.

6. At the command prompt type the following commands and press **Enter** after each command:

   ```
   gpresult /H GPReport.html
   
   GPReport.html
   ```

7. An HTML report displays. Review the information to validate which GPOs were applied, which GPOs were filtered, and if there are any errors reported. 

8. You will notice in both reports that the Contacts App Policy has not been applied to Paul. You will now use the Group Policy Management console to verify your findings.

9. Close all open windows and sign out of SEA-CL1.

### Task 2: Modify Group Policy Object settings  

1. Switch to **SEA-SVR1** and select **Start**, and then select **Server Manager**.

2. Select **Tools** and then select **Group Policy Management**.

3. Maximize the Group Policy Management window. In the console tree, expand **Forest:Contoso.com**, expand **Domains**, and then expand **Contoso.com**. Select the **Group Policy Objects** node. Notice the **Contacts App Policy**.

4. Double-click the **Contacts App Policy**.

5. Review the Scope tab for two issues related to the policy setting. Can you identify the issues? 

   > Not only is the policy not linked to the Sales OU, but the security filtering is not configured correctly. Security Filtering must be applied to the Sales Managers group.

6. In the details pane, under **Security Filtering**, select **Add**.

7. In the **Select User, Computer, or Group** box, under **Enter the object name to select (examples)** enter **Sales Managers**, click **Check Names** and then select **OK**.

8. In the Group Policy Management console, right-click the **Sales** OU, and then select **Link an existing GPO**.

9. Select **Contacts App Policy** and then select **OK**.

10. Close all open windows on SEA-SVR1.

### Task 3: Validate the Group Policy Object settings  

1. Switch to **SEA-CL1** and sign in as **Contoso\Paul** with the password of **Pa55w.rd**.

2. On the SEA-CL1 desktop, take note of the shortcut to Contact Apps. 

3. Sign out of SEA-CL1 and then sign in as **Contoso\Ben** with the password of **Pa55w.rd**.

   > On the SEA-CL1 desktop, notice that there is no shortcut. Ben is a member of the Sales OU, but is not a member of the Sales Managers group. The Sales Managers group is the only group that is filtered for the Contact Apps policy GPO.

5. Sign out of SEA-CL1.

**Results**: After completing this exercise, you will have successfully addressed the Sales Managers GPO issue.

**END OF LAB**

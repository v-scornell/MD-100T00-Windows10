# Practice Lab: Recovering Windows by using a System Protection and a Restore Point

## Summary

During this lab, you will recover a Windows client device by using System Protection and Restore Point.

### Scenario

A colleague reports that after attempting to install a new printer on SEA-CL1, all of the Print drivers are no longer available. You remember that a System Restore Point had been previously created that enables you to return to a previous working state. You decide to use System Protection and restore SEA-CL1 to that previous state.

### Task 1: Configure System Protection and Create a Restore Point

1. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password of **Pa55w.rd**.

2. On the taskbar, select **Start** and the type **Printers**.

3. In the search results, under **Printers & scanners**, select **Open**. The **Settings** window opens at the **Printers & scanners** page.

   > Notice the four printers that are configured (Fax, Microsoft Print to PDF, Microsoft XPS Class Driver ,and Microsoft XPS Document Writer.)

4. In the **Settings** window, select **System** and then scroll down and select **About**.

5. Under the **Device specifications** section, next to **Related links** select **System protection**. The **System Properties** box opens on the **System Protection** tab.

6. On **System Protection** tab, in the **Protection Settings** section, select **Local Disk (C:) (System)**, select **Configure**, select **Turn on system protection**, move the **Max Usage** slider to **5%**, and then select **OK**.

7. Under **Protection Settings**, next to **Create a restore point right now for the drives that have system protection turned on**, select **Create**.

8. In the **Create a restore point** box, enter **Initial Restore Point**, and then select **Create**.

   > System Protection creates a new restore point.

9. When the the System Protection message box is displayed, select **Close**.

10. In the **System Properties** box, select **OK**, and then close the **Settings** window.

### Task 2: Simulate the Problem

1. On SEA-CL1, open File Explorer, and browse to **D:\\Labfiles\Mod13**.

2. In the Mod13 folder, double-click **scenario1.vbs**. 

3. At the Windows Script Host message, select **OK**, and then close File Explorer.

### Task 3: Perform a System Restore

1. On the taskbar, select **Start** and the type **Printers**.

2. In the search results, under **Printers & scanners**, select **Open**. The **Settings** window opens at the **Printers & scanners** page.

   > Notice that the four printers are no longer available. You will use System Restore to restore SEA-CL1 to a previous known good state.)

3. In the **Settings** window, select **System** and then scroll down and select **About**.

4. Under the **Device specifications** section, next to **Related links** select **System protection**. The **System Properties** box opens on the **System Protection** tab.

5. On **System Protection** tab, under **System Restore**, select **System Restore**. The System Restore wizard starts.

6. On the **Restore system files and settings** page, select **Next**.

   > Notice the restore points that have been saved on SEA-CL1.

7. On the **Restore your computer to the state it was in before the selected event** page, select **Initial Restore Point**, and then select **Scan for affected programs**.

   > System Restore scans for any affected programs or drivers as a result of reverting to the selected the restore point.

8. On the **System Restore** window, confirm that no programs or drivers will be deleted and then select **Close**.

9. On the **Restore your computer to the state it was in before the selected event** page, select **Initial Restore Point**, and then select **Next**.

10. On the **Confirm your restore point** page, confirm the information and then select **Finish**.

11. On the Warning message, select **Yes**.

    > System restore begins to restore the Initial Restore Point. SEA-CL1 will also restart during this process. This will take a few minutes to complete.

12. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password of **Pa55w.rd**.

13. When the the System Restore message box is displayed, select **Close**.

14. On the taskbar, select **Start** and the type **Printers**.

15. In the search results, under **Printers & scanners**, select **Open**. The **Settings** window opens at the **Printers & scanners** page.

    > Notice the four printers have been restored to the previous state (Fax, Microsoft Print to PDF, Microsoft XPS Class Driver ,and Microsoft XPS Document Writer.)

16. Close the **Settings** window and sign out of SEA-CL1.

**Results**: After completing this exercise, you should have successfully used System Protection and recovered a Windows client to a previous System Restore Point.

**END OF LAB**

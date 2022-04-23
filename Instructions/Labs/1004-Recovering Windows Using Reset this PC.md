# Practice Lab: Recovering Windows using Reset This PC

## Summary

During this lab you will recover a Windows client device using Reset This PC.

### Scenario

You discover that SEA-CL2 is having intermittent issues. Repeated attempts have been made to correct the issues, but have been unsuccessful. You've decided to try resetting the PC. You would like to still retain the user files on the PC.

### Task 1: Use the Reset this PC option

1. Sign in to **SEA-CL2** as **Contoso\\Administrator** with the password of **Pa55w.rd**.

2. On **SEA-CL2**, right-click the desktop, point to **New**, select **Text Document**, type **Report** as its name, and then press Enter.

3. Right-click the **Start** icon, select **Windows Terminal**.

4. In the Windows PowerShell prompt, type `sysdm.cpl` and then press **Enter**.

5. Verify that the device name is **SEA-CL2** and that it is in the **Contoso.com** domain.

6. Select **Start**, select **Settings**, and then select **System**.

7. In the **System** navigation pane, select **Recovery**.

8. On the Recovery page, next to **Reset this PC**, select **Reset PC**.

9. On the Reset this PC dialog box, select **Keep my files**.

10. When prompted to select where to reinstall Windows from, select **Local reinstall**, and then select **Next**.

11. On the Ready to reset this PC page, select **View apps that will be removed**. Take note of the apps and then select **Back**.

12. On the Ready to reset this PC page, select **Reset**.

13. Wait for the reset to complete. It will take a while to complete.

    > Your instructor may choose to continue with the next module while this task completes. Be sure to return to complete Task 2 when the next lab session begins.

### Task 2: Verify that Reset this PC was successful

1. Sign in to **SEA-CL2** as **Contoso\\Administrator** with the password of **Pa55w.rd**.

2. Verify that the file **Report.txt** is still available on the desktop.

3. On the desktop, double-click the **Removed Apps** report and verify the apps that have been removed while resetting the PC.

4. Close Microsoft Edge.

5. Right-click the **Start** icon, select **Windows Terminal**.

6. In the Windows PowerShell prompt, type `sysdm.cpl` and then press **Enter**.

7. Verify that the device name is SEA-CL2 and that it is in the Contoso.com domain.

8. Close all open windows.

9. Sign out of SEA-CL2.

**Results**: After completing this exercise, you will have successfully recovered SEA-CL2 by using Reset This PC.

**END OF LAB**

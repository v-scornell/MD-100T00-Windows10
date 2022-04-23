# Practice Lab: Using Windows RE and Advanced Startup to recover from Boot Failures

## Summary

In this lab you work with the Windows Recovery Environment (RE) and use System Configuration and Startup Settings to access advanced startup options.

### Scenario

You need to test and validate the features available for when you need to recover from boot failures on a Windows client. You will access Windows RE to identify the recovery options that are available. You will also use System Configuration and Startup Settings to access the advanced startup options.

### Task 1: Use Windows Recovery Environment

1. Switch to SEA-CL2.

2. At the sign-in page, hold down the SHIFT key on your keyboard, select the **Power** button, and then select **Restart**.

   > Windows restarts in the Windows recovery environment

3. On the **Choose an option** page, select **Troubleshoot**.

4. On the **Troubleshoot** page, select **Advanced options**.

5. On the **Advanced options** page, notice the six tools that are available.

6. Select **Command Prompt**.

7. At the command prompt, enter **diskpart**, and then select Enter.

8. At the command prompt, enter **list disk**, and then select Enter.

9. At the command prompt, enter **list volume**, and then select Enter. 

   > Notice that Drive C is the 126 GB NTFS volume. This is the volume that contains the Windows files.

10. At the command prompt, enter **exit**, and then select Enter.

11. At the command prompt, enter **C:**, and then select Enter.

12. At the command prompt, enter **dir**, and then select Enter. This is the system drive.

13. At the command prompt, enter **cd\\windows\\system32**, and then select Enter.

14. At the command prompt, enter **net start**, and then select Enter. A list of running services is returned.

15. At the command prompt, enter **sc query**, and then select Enter. A list of services and their current status is returned.

16. At the command prompt, enter **regedit**, and then select Enter. The Registry Editor opens.

17. Close the Registry Editor.

18. At the command prompt, enter **exit**, and then select Enter.

19. On the Choose an option page, select **Troubleshoot**.

20. On the **Troubleshoot** page, select **Advanced options**.

21. On the Advanced options page, select **Startup Repair**. Automatic startup repair begins.

22. On the Startup Repair page, notice the log file (C:\\Windows\\System32\\Logfiles\\Srt\\SrtTrail.txt) mentioned in the message.

23. Select **Advanced options**.

24. On the Choose an option page, select **Continue**.

25. Sign in as **Contoso\\Administrator** by using the password **Pa55w.rd**.

26. On the taskbar, select **File Explorer**.

27. In File Explorer, navigate to **C:\\Windows\\System32\\Logfiles\\Srt**.

28. In the **Srt** folder, open **SrtTrail.txt**.

29. Examine the file for any errors. (ignore any errors for this lab scenario.)

30. Close the file, and then close File Explorer.

### Task 2: Use System Configuration to modify boot options

1. On SEA-CL2, select **Start**, type **msconfig.exe**, and then select Enter. The System Configuration application opens.

2. In the System Configuration dialog box, select the **Boot** tab.

3. On the Boot tab, select the **Safe boot** check box, and then select **OK**.

4. In the System Configuration dialog box, select **Restart**.

5. When the computer restarts, sign in as **Contoso\\Administrator** by using the password **Pa55w.rd**. 

   > Notice that the desktop now displays Safe Mode in each corner.

6. Right-click **Start** or activate its context menu, and then select **Run**.

7. In the Run box, enter **msconfig.exe**, and then select Enter.

8. In the System Configuration dialog box, on the General tab, select **Normal startup**, and then select **OK**.

9. In the System Configuration dialog box, select **Restart**.

10. When the computer restarts, sign in as **Contoso\\Administrator** by using the password **Pa55w.rd**. 

    > Notice that the Windows operating system starts normally.

11. On SEA-CL2, select **Start**, and then select **Settings**.

12. In **Settings**, select **System** and then select **Recovery**.

13. In the results pane, next to **Advanced startup**, select **Restart now**.

14. At the message prompt, select **Restart now**.

15. On the Choose an option page, select **Troubleshoot**.

16. On the Troubleshoot page, select **Advanced options**.


17. On the Advanced options page, select **Startup Settings**.

18. On the Startup Settings page, select **Restart**. 

    > Notice the Startup Settings are similar to what was available in the System Configuration tool.

19. On the Startup Settings page, press **Enter** to start normally.

**Results**: After completing this exercise, you should have started Windows RE and used System Configuration and Startup Settings to access advanced startup options.

**END OF LAB**

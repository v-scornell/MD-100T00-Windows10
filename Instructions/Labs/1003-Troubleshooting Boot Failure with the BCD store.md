# Practice Lab: Troubleshooting Boot Failure with the BCD store

## Summary

In this lab, you will troubleshoot startup issues with the Windows Boot Configuration Data (BCD) store.

### Scenario

A user named Jim has reported that while attempting to configure a dual-boot Windows environment, SEA-CL2 will no longer boot into any operating system. You need to identify and resolve the issue so that Jim can have a functioning Windows 11 device.

### Task 1: Simulate the issue

1. Sign in to **SEA-CL2** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. Open File Explorer and then browse to **C:\\Labfiles\\Mod12**.

3. Run the **C:\\Labfiles\\Mod12\\scenario1.vbs** script.

4. Wait for SEA-CL2 to restart.

### Task 2: Resolve the issue

1. Attempt to resolve the issue by using your knowledge of boot failure troubleshooting . If you are unable to resolve the problem, escalate it by asking your instructor for additional guidance. The following steps provide the troubleshooting steps and solution to the issue.

2. On SEA-CL2, read the information presented on the **Recovery** screen.

3. Press **F1** on your keyboard to boot into the Recovery Environment.

   > Note: If you take too long to press F1, the machine will automatically turn off. At this point select Start to start the machine and then press F1 to enter the Recovery Environment.

4. At the **Choose your keyboard** layout, select **US**.

   > The Windows recovery environment starts.

5. On the Choose an option page, select **Troubleshoot**.

6. On the Advanced options page, select **Command Prompt**. 

7. At the command prompt, enter **bcdedit /enum**, and then select Enter. 

   > This lists the available boot options in the store. Notice that there is no default entry to the C:\Windows environment.

8. At the command prompt, enter **bootrec /rebuildbcd**, and then select Enter. 

   > This command attempts to rebuild the boot store automatically, however it cannot find a Windows installation to rebuild. We will use diskpart to verify that the original Windows installation is available.

9. At the command prompt, enter **diskpart**, and then press Enter.

10. At the diskpart command, type **list disk** and press Enter. Notice there is only one disk on the system.

11. At the diskpart command, type **select Disk 0** and press Enter.

12. At the diskpart command, type **list volume**.

    This command lists the volumes on Disk 0. Notice that C is labeled on a Hidden drive. Also D is labeled for the DVD-ROM. Also notice that Volume 1 is a 126 GB NTFS partition. This is the original Windows installation. We need to give it a drive letter so that we can fix the BCD.

13. At the diskpart command, type **Select volume 1** and press Enter.

14. At the diskpart command, type **Assign letter = E:** and press Enter.

15. At the diskpart command, type **list volume**. Notice that Volume 1 now has a drive letter E.

16. At the diskpart command, type **exit**.

17. At the command prompt, enter **bootrec /scanos**, and then press Enter. 

    > Notice that a Windows installation is now identified.

18. At the command prompt, enter **bcdboot E:\Windows** and press Enter.

19. At the command prompt, enter **Exit** and press Enter.

20. At the Choose an option screen, select **Continue** to exit and continue to Windows 11.

21. Sign in to **SEA-CL2** as **Contoso\\Administrator** with the password **Pa55w.rd**.

    > Notice that you can now start and sign in to SEA-CL2. 

22. Select Start, type **cmd**, and then press Enter to open the command prompt.

23. At the command prompt enter the following command and press Enter.

    ```
    reagentc /info
    ```

    > Notice that the Windows RE status is disabled. We will enable Windows RE for future troubleshooting.

24. At the command prompt, enter the following command  and press Enter.

    ```
    reagentc /enable
    
    reagentc /info
    ```

    > Notice that Windows RE is now enabled.

25. Sign out of SEA-CL2.

**Results**: After completing this exercise, you will have identified and fixed the BCD issue on SEA-CL2. The device can now start and sign in to Windows 11 successfully.

**END OF LAB**

# Practice Lab: Troubleshooting Domain Authentication

## Summary

In this lab you will identify, troubleshoot, and remediate authentication and connectivity issues between a Windows client and an Active Directory Domain Services (AD DS) domain.

## Exercise 1: Identifying and Troubleshooting Domain Authentication

### Scenario

A user named Jon has reported that he can no longer sign in to SEA-CL1. He also noticed that the standard departmental desktop Group Policy settings were not applying as usual. You need to troubleshoot and identify the issue that is causing Jon's group policy and sign-in issues.

### Task 1: Simulate the issue

1. Sign in to **SEA-CL1** as **Contoso\\Administrator**  with the password **Pa55w.rd**.

2. Open **File Explorer**, and then browse to **D:\\Labfiles\\Mod02**.

3. Run the **Scenario1.vbs** script.

4. Wait while SEA-CL1 restarts.

### Task 2: Identify the issue

1. Sign in to **SEA-CL1** as **Contoso\\Administrator**  with the password **Pa55w.rd**.

2. Right-click **Start**, and then select **Windows Terminal (Admin)**.

3. In the Administrator: Windows PowerShell window, type the following command, and then press **Enter**:

```
    gpupdate /force
```

4. Notice that Group Policy fails to update. Read the message for information on how to diagnose the failure.

5. In the Administrator: Windows PowerShell window, type the following command, and then press **Enter**:

```
    GPRESULT /H GPReport.html
```

6. In the Administrator: Windows PowerShell window, type the following command, and then press **Enter**:

```
    .\gpreport.html
```

7. In the html report, select the link that states 6 Errors Detected. Review the information for details on why Group Policy is failing.

8. Close the html report windows.

9. Right-click **Start**, and then select **Event Viewer**.

10. In the Event Viewer, expand **Windows Logs**, and then select **System**. Review events related to the GroupPolicy source with Event ID 1129 and 1006.

11. Close Event Viewer and sign out of SEA-CL1.

12. Attempt to sign in to **SEA-CL1** as **Contoso\\Jon**  with the password **Pa55w.rd**. Take note of the error message and then select **OK**.

13. Discuss with your class on what might be the issue based upon your investigation.

### Task 3: Remediate the issue

1. Sign in to **SEA-CL1** as **Contoso\\Administrator**  with the password **Pa55w.rd**.

2. Right-click **Start**, and then select **Windows Terminal (Admin)**.

3. In the Administrator: Windows PowerShell window, type the following command, and then press **Enter**:

```
    Reset-ComputerMachinePassword -Server SEA-DC1 -Credential Contoso\Administrator
```

4. At the Windows PowerShell credential request prompt, enter **Pa55w.rd** for the password.

5. In the Administrator: Windows PowerShell window, type the following command, and then press **Enter**:

```
    gpupdate /force
```

6. Notice that Group Policy now updated successfully.

7. Sign out of SEA-CL1.

8. Attempt to sign in to **SEA-CL1** as **Contoso\\Jon**  with the password **Pa55w.rd**. Notice that the user can sign-in successfully.

9. Sign out of SEA-CL1.

**Results**: After completing this exercise you will have identified the issue that is causing Jon to have group policy and sign-in issues. You also remediated the issue by performing a PowerShell command that resets the machine password with the Active Directory domain controller.

**END OF LAB**

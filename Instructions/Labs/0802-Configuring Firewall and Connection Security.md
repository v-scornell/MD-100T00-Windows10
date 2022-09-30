# Practice Lab: Configuring Firewall and Connection Security

## Summary

In this exercise you will create and configure firewall rules to block and allow specific service connections to a device. You will also create and configure connection security rules to encrypt network traffic between Windows devices.

## Exercise 1: Creating and Testing Inbound Firewall Rules  

### Scenario

Users that work on SEA-CL2 are not allowed to remote desktop into SEA-CL1. You need to verify that remote desktop currently is allowed and then configure a firewall rule on SEA-CL1 that will block remote desktop connections. You will leave the Remote desktop service enabled to allow for other device connections to be configured at a later time.

### Task 1: Validate existing functionality

1. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. Right-click Start and then select **System**.

3. On the System page, select **Advanced system settings**.

4. On the System Properties box, select the **Remote** tab.

5. In the Remote Desktop section, select **Allow remote connections to this computer** and then select **OK**.

6. Close the **Settings** window.

7. Switch to **SEA-CL2**.

8. Sign in to **SEA-CL2** as **Contoso\\Administrator** with the password **Pa55w.rd**.

9. Select **Start**, type **mstsc.exe**, and then press **Enter**. The Remote Desktop Connection app opens.

10. In the Computer box, type **SEA-CL1**, and then select **Connect**. The Windows Security dialog box displays asking for credentials to connect to SEA-CL1. This indicates successful connectivity to SEA-CL1.

11. In the Windows Security dialog, select **Cancel**.

### Task 2: Create an inbound rule

1. Switch to **SEA-CL1**.

2. On SEA-CL1, select **Start**, and type **Windows Firewall**.

3. In the results pane, select **Windows Defender Firewall**.

4. In Windows Defender Firewall, in the left pane, select **Advanced settings**, select **Inbound Rules**, and then select **New Rule**.

5. In the New Inbound Rule Wizard window, select **Predefined**, select the **drop-down list**, select **Remote Desktop**, and then select **Next**.

6. On the Predefined Rules page, select the check box next to all available rules, and then select **Next**.

7. On the Action page, select **Block the connection**, and then select **Finish**.

8. Minimize the Windows Defender Firewall with Advanced Security window.

### Task 3: Test the rule ###

1. Switch to **SEA-CL2**.

2. If necessary, select **Start**, type **mstsc.exe**, and then press **Enter**.

3. In the Computer box, type **SEA-CL1**, and then select **Connect**. Notice that the connection attempt fails and displays a Remote Desktop Connection error message.

4. In the Remote Desktop Connection error message window, select **OK**.

5. Close all open windows.

**Results**: After completing this exercise, you will have created and verified inbound firewall rules.

## Exercise 2: Creating and Testing Outbound Firewall Rules ##

### Scenario

SEA-SVR1 also needs to be configured to allow remote desktop connections, however SEA-CL1's firewall configuration should not allow any user to use a remote desktop connection to SEA-SVR1 from SEA-CL1. You will configure an outbound firewall rule on SEA-CL1 to prevent remote desktop connections to the server.

### Task 1: Test existing functionality ###

1. Switch to **SEA-SVR1** and sign in as **Contoso\\Administrator** with the password **Pa55w.rd**

2. Select **Start**, type **control**, and then select **Control Panel**.

3. In the Control Panel, select **System and Security**, and then under **System**, select **Allow remote access**.

4. On the **Remote** tab, under **Remote Desktop**, verify that **Allow remote connections to this computer** is selected.

5. Select **OK** to close the **System Properties** window and then close the Control Panel.

6. Switch to **SEA-CL1**.

7. Select **Start**, type **mstsc.exe**, and then press **Enter**.

8. In the Computer box, type **SEA-SVR1**, and then press **Enter**. The Windows Security dialog box displays asking for credentials to connect to SEA-SVR1. This indicates successful connectivity to SEA-SVR1.

9. In the Windows Security dialog, select **Cancel**.

10. Close Remote Desktop Connection.

### Task 2: Create an outbound rule

1. On **SEA-CL1**, on the taskbar, select the **Windows Defender Firewall with Advanced Security** window, and then select **Outbound Rules**.

2. In the Actions pane, select **New Rule**.

3. On the Rule Type page, verify that you are creating a **Program** rule, and then select **Next**.

4. On the Program page, browse and select **C:\\Windows\\System32\\mstsc.exe**, select **Open**, and then select **Next**.

5. On the Action page, verify that the action is **Block the Connection**, and then select **Next**.

6. On the Profile page, verify that **all profiles are checked**, and then select **Next**.

7. On the Name page, type **Block Outbound RDP to SEA-SVR1** in the Name box, and then select **Finish**.

8. In the Windows Defender Firewall with Advanced Security window, select the **Block Outbound RDP to SEA-SVR1** rule, and then in the Actions pane, select **Properties**.

9. Select the **Scope tab**, and then under the **Remote IP address heading**, select the **These IP addresses** option.

10. Under the Remote IP address heading, select **Add**, in the This IP address or subnet box, type **172.16.0.11**, and then select **OK**.

11. In the Block Outbound RDP to SEA-SVR1 Properties dialog box, select **OK**.

### Task 3: Test the rule ###

1. On SEA-CL1, select **Start**, type **mstsc.exe**, and then press **Enter**.

2. In the Computer box, type **SEA-SVR1**, and then press **Enter**. Notice that the connection attempt fails and displays a Remote Desktop Connection error message.

3. In the Remote Desktop Connection dialog box, select **OK**.

4. **Close** all open windows.

**Results**: After completing this exercise, you will have created and tested outbound firewall rules.

## Exercise 3: Creating Connection Security Rules ##

### Scenario

Your manager wants you to ensure that all network traffic between SEA-CL1 and SEA-CL2 is encrypted. You need to configure a connection security rule with the setting "Require authentication for inbound connections and request authentication for outbound connections" enabled on both devices.

### Task 1: Verify that communications are not secure ###

1. Sign in to **SEA-CL2** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. Right-click **Start**, and then select **Windows Terminal (Admin)**.

3. In the Windows PowerShell window, type the following command and then press **Enter**

```
ping SEA-CL1
```

4. Verify that the ping generated four Reply messages.

5. Select **Start**, type **firewall** and select **Windows Defender Firewall**.

6. In the left pane, select **Advanced settings**.

7. In the left pane, expand **Monitoring,** and then expand **Security Associations**.

8. Select **Main Mode**, and then examine the information in the center pane.

   _**Note**: No information should be present._

9. Select **Quick Mode**, and then examine the information in the center pane.  

   _**Note**: No information should be present._

10. Switch to **SEA-CL1**. If necessary, sign in to **SEA-CL1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

11. Right-click **Start**, and then select **Windows Terminal (Admin)**.

12. To examine the Main Mode Security Associations (SAs), at the Windows PowerShell prompt, type the following cmdlet, and then press **Enter**:

```
Get-NetIPsecMainModeSA
```

13. To examine the Quick Mode SAs, at the Windows PowerShell prompt, type the following cmdlet, and then press **Enter**:

```
Get-NetIPsecQuickModeSA
```

**Note**: Running each command should produce no result.

### Task 2: Create the Connection Security Rule

1. On **SEA-CL1** select **Start**, type **firewall** and select **Windows Defender Firewall**.  

2. In the left pane, select **Advanced settings**, and then select **Connection Security Rules**.  

3. In the Actions pane, select **New Rule**.

4. On the Rule Type page, verify that **Isolation** is selected, and then select **Next**.

5. On the Requirements page, select **Require authentication for inbound connections and request authentication for outbound connections**, and then select **Next**.

6. On the Authentication Method page, select **Computer and user (Kerberos V5)**, and then select **Next**.

7. On the Profile page, select **Next**.

8. On the Name page, in the Name text box, type **Authenticate all inbound connections**, and then select **Finish**.

9. Close the Windows Defender Firewall with Advanced Security window.

10. Switch to **SEA-CL2**.

11. In the Windows Defender Firewall with Advanced Security window, in the left pane select **Connection Security Rules**.

12. In the Actions pane, select **New Rule**.

13. On the Rule Type page, verify that **Isolation is selected**, and then select **Next**.

14. On the Requirements page, select **Require authentication for inbound connections and request authentication for outbound connections**, and then select **Next**.

15. On the Authentication Method page, select **Computer and user (Kerberos V5)**, and then select **Next**.

16. On the Profile page, select **Next**.

17. On the Name page, in the Name text box, type **Authenticate all inbound connections**, and then select **Finish**.

### Task 3: Verify the rule, and monitor the connection ###

1. On SEA-CL2, in the Windows PowerShell window, type the following command and then press **Enter**

```
ping SEA-CL1
```

2. Verify that the ping generated four reply messages.

3. In the Windows Defender Firewall with Advanced Security window, in the left pane expand **Monitoring,** and then expand **Security Associations**.

4. Select **Main Mode**, and then examine the information in the center pane.

5. Select **Quick Mode**, and then examine the information in the center pane.

6. **Close** all open windows.

7. Switch to **SEA-CL1.**

8. To examine the Main Mode Security Associations (SAs), at the Windows PowerShell command prompt, type the following cmdlet, and then press **Enter**:

```
Get-NetIPsecMainModeSA
```

9. Review the result.

10. To examine the Quick Mode SAs, at the command prompt, type the following cmdlet, and then press **Enter**:

```
Get-NetIPsecQuickModeSA
```

11. Review the result and then close all open windows.

12. Sign out of SEA-CL1 and SEA-CL2.

**Results**: After completing this exercise, you will have created and tested connection security rules.

**END OF LAB**

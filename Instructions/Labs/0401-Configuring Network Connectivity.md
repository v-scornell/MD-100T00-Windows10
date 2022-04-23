# Practice Lab: Configuring Network Connectivity

## Summary

In this lab, you will identify IPv4 settings and validate connectivity on a Windows device. You will also configure a Windows device to automatically obtain IPv4 settings from a DHCP service.

## Exercise 1: Verifying and Testing IPv4 Settings

### Scenario

You need to identify the current static IPv4 settings on SEA-CL1. You also need to test connectivity from SEA-CL1 to SEA-DC1.

### Task 1: Verify IPv4 settings from Settings and the Network and Sharing Center

1. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. Select the **Start** button, and then select **Settings**.

3. In the **Settings** window, select **Network & internet** and then in the status area select **Properties**.

4. Identify the **IP settings** and **Properties** for the network adapter. The following information should be available:

   - IP assignment
   - IPv4 address
   - IPv4 mask
   - IPv4 gateway
   - DNS server assignment
   - IPv4 DNS servers

   *Also take note that the IP assignment is set to Manual, which indicates that this is a static IP address assignment.*

5. Next to **IP address**, select **Edit**. Notice that you can modify the IPv4 and IPv6 settings.

6. Select **Cancel** to close the **Edit IP settings** window.

7. Next to IPv4 DNS servers, select Edit. Notice that you can modify the DNS settings for both IPv4 and IPv6.

8. Select **Cancel** to close the **Edit DNS settings** window.

9. In the **Settings** window, select **Network & internet**.

10. In the Status details pane, select **Advanced network settings**. 

11. In **Advanced network settings**, select **More network adapter options**. The Network Connections window opens.

12. In the Network Connections window, right-click **Ethernet** and then select **Status**.

13. In the **Ethernet Status** dialog box, select **Details**. This window displays the same configuration information for this adapter as the Settings status page.

14. In the **Network Connection Details** window, select **Close**.

15. In the **Ethernet Status** dialog box, select **Properties**. You can configure protocols in this window.

16. Select **Internet Protocol Version 4 (TCP/IPv4)**, and then select **Properties**.

    _Note: You can configure the IP address, subnet mask, default gateway, and Domain Name System (DNS) servers in this window._

17. Select **Cancel** and then close all open windows without modifying any settings.

### Task 2: Verify IPv4 settings from the command line

1. On SEA-CL1, select **Start**, and then type **PowerShell**. Windows PowerShell displays in the search results.

2. Under Windows PowerShell, select **Run as administrator**.

3. At the Windows PowerShell command prompt, type following command, and then press **Enter**.

```
    Get-NetIPAddress
```

_Note: The IPv4 address from the Ethernet interface should match what you identified earlier._

3. At the Windows PowerShell command prompt, type the following command, and then press **Enter**.

```
    netsh interface ipv4 show config
```

_Note: The current IPv4 configuration is displayed and should match what you identified earlier._

4. At the Windows PowerShell command prompt, type the following command, and then press Enter.

```
    ipconfig /all
```

_Note: Again, the information should match what you identified earlier._
5. Leave the **Administrator: Windows PowerShell** window open.

### Task 3: Test connectivity

1. At the Windows PowerShell command prompt, type the following command, and then press **Enter**.

```
    Test-Connection SEA-DC1
```

2. At the Windows PowerShell command prompt, type the following command, and then press **Enter**.

```
    Ping SEA-DC1
```

3. At the Windows PowerShell command prompt, type type the following command, and then press **Enter**.

```
   PathPing SEA-DC1
```

4. Observe and describe the differences between the three connectivity tests performed.

   _Note: Test-Connection and Ping provides information on time and success of connectivity directly to a target host. PathPing provides statistics on how many connections it takes to route to a target host._

5. Close the Windows PowerShell window.

**Results**: After completing this exercise you have verified the IPv4 settings of a windows device and used various tools to test connectivity.

## Exercise 2: Configuring Automatic IPv4 Settings

### Scenario

Your network administrative team has configured DNS and DHCP services located on SEA-DC1. You need to reconfigure SEA-CL1 to obtain its IPv4 settings using the DHCP service. You will then test and verify the connectivity between SEA-CL1 and SEA-DC1 using the newly obtained IPv4 address settings.

### Task 1: Reconfigure the IPv4 settings

1. On **SEA-CL1**, select the **Start** button, and then select **Settings**.

2. Select **Network & internet**.

3. In **Network and internet**, select **Ethernet**.

4. Next to **IPv4 address**, select **Edit**.

5. Under **Edit IP settings**, select the drop-down menu, select **Automatic (DHCP)**, and then select **Save**.

   > Notice that the DNS server assignment also changes to Automatic (DHCP).

6. In the **Settings** window, select **Network & internet**.

7. In the Status details pane, select **Advanced network settings**. 

8. In **Advanced network settings**, select **More network adapter options**. The Network Connections window opens.

9. In the Network Connections window, right-click **Ethernet** and then select **Status**.

10. In the **Ethernet Status** dialog box, select **Details**. Notice that DHCP is enabled, and that the IP address of the DHCP server displays.

11. Close all open windows on SEA-CL1.

12. On SEA-CL1, select **Start**, and then type **PowerShell**. Windows PowerShell displays in the search results.

13. Under Windows PowerShell, select **Run as administrator**.

14. At the Windows PowerShell command prompt type the following command, and then press **Enter**.

```
    ipconfig /all
```

13. Verify that the IPv4 address is obtained from DHCP.

### Task 2: Test connectivity

1. At the Windows PowerShell command prompt, type type the following command, and then press **Enter**.

```
    Test-Connection SEA-DC1
```

_Note: You should receive four replies from SEA-DC1._
2. Close all open windows.
3. Sign out of SEA-CL1.

### Task 3: View the impact on the DHCP server

1. Switch to **SEA-SVR1**.

2. Sign in to SEA-SVR1 as **Contoso\\Administrator** with the password **Pa55w.rd**.

3. Select **Start** and then select **Server Manager**.

4. In **Server Manager**, select **All Servers**, right-click **SEA-DC1**, and then select **DHCP Manger**.

5. In **DHCP**, expand **SEA-DC1.Contoso.com**, expand **IPv4**, expand **Scope [172.16.0.0] Contoso**, and then select **Address Leases**.

6. In the details pane, you should see the address lease for the SEA-CL1 Windows client.

7. Close the DHCP window and then sign out of SEA-SVR1.

**Results**: After completing this exercise you have configured a Windows device to automatically obtain IPv4 settings from a DHCP service.

**END OF LAB**

# Practice Lab: Configuring and Testing Name Resolution

## Summary

In this lab, you will verify and manage name resolution for a Windows network client. You will also test name resolution by using command line tools, DNS, and a hosts file entry.

### Prerequisites

To following lab(s) must be completed before this lab:

- 0501-Configuring Network Connectivity - On SEA-CL1, DHCP should be enabled for the Ethernet connection.

## Exercise 1: Verify and Manage Name Resolution

### Scenario

You need to check and verify current DNS settings on SEA-CL1. You will also test out command line tools used to view and clear the DNS client cache.

### Task 1: Verify current DNS settings

1. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. Right-click **Start**, and then select **Windows Terminal (Admin)**.

3. At the Windows PowerShell command prompt, type the following command, and then press **Enter**.  

```
    ipconfig /all
```

_Note: DHCP should be enabled from the previous lab. Take note of the IP address of the DHCP server and the IP address of the DNS server._

4. At the Windows PowerShell command prompt, type the following command, and then press **Enter**.  

```
    Get-NetIPConfiguration 
```

_Note: The PowerShell command also provides IP address information._

### Task 2: View and clear the DNS resolver cache

1. At the Windows PowerShell command prompt, type the following command, and then press **Enter**. This will resolve SEA-SVR1.contoso.com to an IP address and store the results in the DNS resolver cache.

```
   ping SEA-SVR1.contoso.com
```

2. At the Windows PowerShell command prompt, type the following command, and then press **Enter**. This will resolve SEA-DC1.contoso.com to an IP address and store the results in the DNS resolver cache.

```
   Test-Connection SEA-DC1.contoso.com
```

3. At the Windows PowerShell command prompt, type the following command, and then press **Enter**. This displays the current DNS resolver cache.

```
   ipconfig /displaydns
```

4. At the Windows PowerShell command prompt, type the following command, and then press **Enter**. This displays the current DNS resolver cache using a PowerShell command.

```
   Get-DnsClientCache
```

5. At the Windows PowerShell command prompt, type the following command, and then press **Enter**. This flushes the current DNS resolver cache.

```
   ipconfig /flushdns
```

6. At the Windows PowerShell command prompt, type the following command, and then press **Enter**. This flushes the current DNS resolver cache using a PowerShell command.

```
   Clear-DnsClientCache
```

   _Note: It is not necessary to run this in addition to the preceding command._

7. At the Windows PowerShell command prompt, type the following command, and then press **Enter**. This verifies that you have no entries in the cache.

```
   ipconfig /displaydns
```

**Results**: After completing this exercise you have verified current DNS settings on SEA-CL1 and used command line tools to view and clear the DNS client cache.

## Exercise 2: Testing Name Resolution

### Scenario

A user reports that SEA-CL1 cannot connect to www.Contoso.com or intranet.Contoso.com. To address the issue, you decide to add www to the hosts file along with the SEA-SVR1.contoso.com IP address. You will also add an alias DNS record for intranet.Contoso.com that resolves to SEA-CFG1.contoso.com. Finally you will verify name resolution and connectivity.

### Task 1: Create and test a hosts file entry

1. On SEA-CL1, at the Windows PowerShell command prompt, type the following command, and then press **Enter**.

```
    ping www
```

2. At the Windows PowerShell command prompt, type the following command, and then press **Enter**.

```
    ping intranet
```

_Note:  Neither name is reachable because www and intranet cannot be resolved to a valid IP address._

3. At the Windows PowerShell command prompt, type the following command, and then press **Enter**.

```
    notepad C:\windows\system32\drivers\etc\hosts
```

4. Scroll to the end of the file, type the following, and then press **Enter**.

```
    172.16.0.11 www
```

5. Select **File**, and then select **Save**.

6. Close Notepad.

7. At the Windows PowerShell command prompt, type the following command, and then press **Enter**.

```
    Test-Connection www
```

8. At the Windows PowerShell command prompt, type the following command, and then press **Enter**.

```
    Get-DnsClientCache
```

9. View the www record in the cache.

10. Leave PowerShell open.

### Task 2: Add a DNS record

1. Sign in to **SEA-SVR1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. Select **Start** and then select **Server Manager**.

3. In Server Manager, select **All Servers**.

4. Right-click **SEA-DC1**, and then select **DNS Manager**.

5. Select **SEA-DC1.Contoso.com**, expand the **Forward Lookup Zones** folder and select **Contoso.com**.

6. Select **Action** in the top menu, then select **New Alias (CNAME)**.

7. In the **Alias Name** field, type **intranet**.

8. In the **Fully Qualified domain name (FQDN) for target host:** field, type **SEA-CFG1.Contoso.com** and select **OK.**

9. Sign out of SEA-SVR1.

10. Switch to **SEA-CL1**.

11. In the PowerShell window, type the following command, and press **Enter**.

```
    ping intranet.Contoso.com
```

10. Verify that intranet.Contoso.com is resolving to SEA-CFG1.contoso.com and IP Address 172.16.0.13.

11. Sign out of SEA-CL1.

**Results**: After completing this exercise you have added a hosts file entry, created a DNS record, and tested name resolution.

**END OF LAB**

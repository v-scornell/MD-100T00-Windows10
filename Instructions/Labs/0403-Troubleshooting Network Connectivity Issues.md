# Practice Lab: Troubleshooting Network Connectivity Issues

## Summary

In this lab, you will troubleshoot network connectivity and name resolution issues.

### Prerequisites

To following lab(s) must be completed before this lab:

- 0401-Configuring Network Connectivity - On SEA-CL1, DHCP should be enabled for the Ethernet connection.
- 0402 - Configuring and Testing Name Resolution - Create the intranet.contoso.com DNS alias record.

## Exercise 1: Resolving network connectivity

### Scenario

A user named Paul has reported that after restarting SEA-CL1, he is no longer able to connect to **\\\\LON-DC1\\Labfiles**. You check with other users, and it seems that whenever anyone restarts their computer, connectivity to the network resource is affected. 

You need to investigate and resolve the issue.

### Task 1: Simulate the issue

1. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. Open File Explorer and then browse to **D:\\Labfiles\\Mod05**.

3. Run the **D:\\Labfiles\\Mod05\\scenario1.vbs** script.

4. Wait for SEA-CL1 to restart.

### Task 2: Resolve the issue

1. Attempt to resolve the issue by using your knowledge of the network services and the tools available for troubleshooting a network environment. If you are unable to resolve the problem, escalate it by asking your instructor for additional guidance. The following steps provide the troubleshooting steps and solution to the issue.

2. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

3. Select **Start**, and then type **cmd**. The Command prompt displays in the search results.

4. Under Command Prompt, select **Run as administrator**.

5. At the command prompt, type the following command, and then press **Enter**.

```
   ipconfig /all
```

> Notice that the IPv4 address has the prefix of 169.254.

6. At the command prompt, type the following command, and then press **Enter**.

```
   ipconfig /renew
```

> Note that the IP renewal is not successful.

7. Switch to **SEA-SVR1**

8. If necessary, select **Start** and then select **Server Manager**.

9. Select **All Servers**, right-click **SEA-DC1**, and then select **DHCP Manager**.

10. In DHCP Manager, select **SEA-DC1.Contoso.com**.

    > Notice that a message displays that the DHCP server cannot be located, and it seems the service is not running.

11. Right-Click **SEA-DC1.Contoso.com**, point to **All Tasks**, and then select **Start**. The DHCP service starts.

12. Sign out of SEA-SVR1.

13. Switch to **SEA-CL1**.

14. At the command prompt, type the following command, and then press **Enter**.

```
   ipconfig /renew
```

> Notice that SEA-CL1 can now renew the IPv4 address.

15. Select **File Explorer** and then browse to **\\\\SEA-DC1\\Labfiles**. You should now be able to access the network resource.
16. Close File Explorer and sign out of SEA-CL1.

**Results**: After completing this exercise you have fixed network connectivity issues to a network resource.

## Exercise 2: Resolving network name resolution

### Scenario

Julia reports that she can no longer access **http://intranet.contoso.com** or **\\\\SEA-SVR1\\Labfiles** from SEA-CL1. Other users in the department can successfully access the site. You need to investigate and resolve the issue. Note: The DNS server IP address is 172.16.0.10. The IP address for SEA-SVR1 is 172.16.0.11.

### Task 1: Simulate the issue

1. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

2. Open File Explorer and then browse to **D:\\Labfiles\\Mod05**.

3. Run the **D:\\Labfiles\\Mod05\\scenario2.vbs** script.

4. Wait for SEA-CL1 to restart.

### Task 2: Resolve the issue

1. Attempt to resolve the issue by using your knowledge of the network services and the tools available for troubleshooting a network environment. If you are unable to resolve the problem, escalate it by asking your instructor for additional guidance. The following steps provide the troubleshooting steps and solution to the issue.

2. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password **Pa55w.rd**.

3. Select **Start**, and then type **PowerShell**. The Windows PowerShell displays in the search results.

4. Under Windows PowerShell, select **Run as Administrator**.

5. At the prompt, type the following command, and then press **Enter**.

```
   ping intranet.contoso.com
```

> Notice that the request times out to confirm that connectivity to intranet.contoso.com has an issue.

6. At the prompt, type the following command, and then press **Enter**.

```
   test-connection SEA-SVR1.contoso.com
```

> Note that the command fails, which confirms that the connection to SEA-SVR1 has an issue.

7. At the prompt, type the following commands, each followed by **Enter**.


```
   test-connection 172.16.0.10
   ping 172.16.0.13
```

> Note that connectivity directly to the IP address of each resource is successful. You identify that the issue must be related to name resolution.

8. At the prompt, type the following command, and then press **Enter**.

```
   Get-DnsClientCache
```

> Notice the records that are returned. Review the records related to intranet.contoso.com and sea-svr1. What do you notice about the IP address for both resources?

9. At the prompt, type the following commands, each followed by **Enter**.

```
   Clear-DnsClientCache
   Get-DnsClientCache
```

> Note that the DNS cache clears most records, however the intranet.contoso.com and the sea-svr1 records still remain with the incorrect IP addresses. What may be causing these records to maintain in the DNS client cache?

10. At the prompt, type the following command and then press **Enter**.


```
notepad C:\windows\system32\drivers\etc\hosts
```

> Note that incorrect entries are listed in the locals hosts file of SEA-CL1.

11. Scroll to the end of the file, delete **172.16.10.10 intranet.contoso.com** and delete **172.16.10.11 sea-svr1**.

12. Save and close the file.

13. At the prompt, type the following command, and then press **Enter**.

```
   ping intranet.contoso.com
```

> Notice that the request fails which confirms that connectivity to intranet.contoso.com still has an issue.

14. At the prompt, type the following command, and then press **Enter**.

```
   test-connection SEA-SVR1.contoso.com
```

> Note that the command fails, which confirms that the connection to SEA-SVR1 still has an issue.

15. At the command prompt, type the following command, and then press **Enter**.


```
   ipconfig /all
```

> Take note of the IP configuration for SEA-CL1. What do you notice about the DNS Servers configuration? It should be 172.16.0.10.

16. On **SEA-CL1**, select the **Start** button, and then select **Settings**.
17. Select **Network & internet**.

18. In **Network and internet**, select **Ethernet**.

19. Next to **IPv4 address**, select **Edit**.

20. Under **Edit IP settings**, select the drop-down menu, select **Automatic (DHCP)**, and then select **Save**.

    > Notice that the DNS server assignment also changes to Automatic (DHCP).

21. Switch to the PowerShell window.

22. At the Windows PowerShell command prompt type the following command, and then press **Enter**.


```
    ipconfig /all
```

> Notice that the IP address for the DNS server is now correctly configured to 172.16.0.10. The DHCP server is configured to provide this information automatically. 

23. At the prompt, type the following command, and then press **Enter**.

```
   ping intranet.contoso.com
```

> Notice that the ping request is now successful with four replies from the server.

24. At the prompt, type the following command, and then press **Enter**.

```
   test-connection SEA-SVR1.contoso.com
```

> Note that the command connects to SEA-SV1 successfully.

25. Close all open windows and sign out of SEA-CL1.


**Results**: After completing this exercise you have fixed network connectivity issues to a network resource.

**END OF LAB**

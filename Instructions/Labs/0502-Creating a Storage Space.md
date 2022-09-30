# Practice Lab: Creating a Storage Space

## Summary

In this lab you configure a storage space that will combine multiple disk drives to one large single disk with resiliency.

### Scenario

The sales department requires a new file share on SEA-WS2 that requires a mirror for resiliency. You have added three new disk drives to SEA-WS2, and have decided to configure a storage space. You will remove the partition from Disk 1 first and then use Disk 1, Disk 2, and Disk 3 to create a two-way mirror storage pool inside a newly created storage space.

### Task 1: Initialize the required disks

1. Sign in to **SEA-WS2** as **.\Admin** with the password **Pa55w.rd**.

2. Right-click **Start**, and then select **Windows Terminal (Admin)**. At the User Account Control, select **Yes**.

3. To remove all data from Disk 1, at the PowerShell Window type the following command and confirm with "Yes":

```
Clear-Disk -Number 1 -RemoveData
```

4. To initialize Disk 1, Disk 2, and Disk 3, at the PowerShell Window type the following command:

```
Get-Disk | Where partitionstyle -eq 'raw' | Initialize-Disk -PartitionStyle MBR
```

5. Close Windows PowerShell.

### Task 2: Create a mirrored storage pool

1. Select **Start**, and then select **Settings**.

2. On the System page, select **Storage**.

3. On the Storage page, select **Advanced storage settings** and then select **Storage Spaces**.

4. On the Storage Spaces page, select **Create a storage pool and Storage Space**. 

   > In the **New storage pool** window notice that Disk 1, Disk 2, and Disk 3 are listed. 

5. Select the check box next to **Disk 1**, **Disk 2**, and **Disk 3**, and then select **Create**.

6. On the **Size & resiliency** section, ensure that **Two-way mirror** is selected and then select **Create**.

7. In the **Drive letter** dropdown field select **E:** and then select **Format**.

   > Review the status information on the Storage Spaces page.

8. Close the Settings app.

### Task 3: Verify the storage space

1. Open File Explorer, right-click **Local Disk (E:)**, and then select **Properties**.

2. Notice that the capacity is approximately 379 gigabytes (GB).

3. Close all open windows.

4. Select **Start**, and then type **Storage spaces**. Select **Manage Storage Spaces** in the list.

5. In the Storage Spaces dialog box expand the **Storage spaces** and the **Physical drives** sections.

6. Close the Storage Spaces window.

7. Sign out of SEA-WS2.

**Results**: After completing this exercise, you will have created and verified a two-way mirror storage space.

**END OF LAB**

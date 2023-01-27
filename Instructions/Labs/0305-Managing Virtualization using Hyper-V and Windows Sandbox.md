# Practice Lab: Managing Virtualization using Hyper-V and Windows Sandbox

## Summary

In this lab you will manage virtualization by using Windows 11 Hyper-V and Windows Sandbox.

## Exercise 1: Creating a Virtual Environment using Hyper-V

### Scenario

You need to enable the Hyper-V feature on SEA-CL1. You will configure Hyper-V to use D:\VirtualMachines as its default file location, and create a new switch named Private Network. Next you will create a new virtual machine named SEA-W10 as a differencing drive based upon a provided VHD file named GoldImage1.vhd. Finally, you will experiment with Checkpoints used to apply and revert to various saved VHD configuration states.

### Task 1: Enable the Windows 11 Hyper-V feature  

1. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password of **Pa55w.rd**.

2. Select **Start**, and then select **Settings**.

3. In the **Settings** window, select **Apps**, and then select **Optional features**.

4. Scroll to the bottom of the Optional features page and then select **More Windows features**. The **Windows Features** dialog box opens.

5. In the **Windows Features** dialog box, select the check box next to **Hyper-V** and then select **OK**.

6. After the changes are applied, select **Restart now**.

7. After SEA-CL1 restarts, sign in as **Contoso\\Administrator** with the password of **Pa55w.rd**.

### Task 2: Configure Hyper-V Settings and Switches  

1. On SEA-CL1, select **Start** and then enter **Hyper-V**. The **Hyper-V Manager** displays in the search results.

2. Select **Hyper-V Manager**. The Hyper-V Manager opens.

3. In Hyper-V Manager, select **SEA-CL1**, and then in the **Actions** pane, select **Hyper-V Settings**.

4. In the **Hyper-V Settings for SEA-CL1**, select **Virtual Hard Disks**, and then in the details pane select **Browse**.

5. Browse to and select the **Allfiles (D:)** drive.

6. Select **New folder** and then name the folder **VirtualMachines**.

7. Select the **VirtualMachines** folder, and then click **Select Folder**.

8. In the **Hyper-V Settings for SEA-CL1**, select **Virtual Machines**, and then in the details pane select **Browse**.

9. Browse to and select the **D:\VirtualMachines** folder and then click **Select Folder**.

10. Select **OK** to close the **Hyper-V Settings for SEA-CL1** window.

11. In the Actions pane, select **Virtual Switch Manager**.

    > Note that a virtual switch named **Default Switch** is created by default. This switch provides access to the host computer's network by using network address translation.

12. Select **New virtual network switch**, and then under **Create virtual switch** select **Private**.

13. Select **Create Virtual Switch**. The **Virtual Switch Properties** page displays.

14. Under **Name**, enter **Private Switch** and then select **Apply**.

15. Select **OK** to close the **Virtual Switch Manager** box.

### Task 3: Configure a Hyper-V virtual hard disk  

1. In Hyper-V Manager, select **SEA-CL1**, and in the **Actions** pane, select **New**, and then select **Hard Disk**.

2. In the New Virtual Hard Disk Wizard, on the Before You Begin page, select **Next**.

3. On the Choose Disk Format page, select **VHD** and then select **Next**.

4. On the Choose Disk Type page, select **Differencing**, and then select **Next**. 

5. On the Specify Name and Location page, in the **Name** field, enter **SEA-W10**. Notice that the Location field defaults to the location configured in Hyper-V Settings. Select **Next**.

6. On the Configure Disk page, select **Browse**, and browse to **D:\Labfiles\VMs**. This is the where the parent virtual hard disk is located. Select **GoldImage1.vhd**, select **Open**, and then select **Next**.

7. On the Completing the New Virtual Hard Disk Wizard page, select **Finish**.

### Task 4: Create a Hyper-V virtual machine

1. In Hyper-V Manager, in the Actions pane, select **New**, and then select **Virtual Machine**.

2. In the New Virtual Machine Wizard, on the Before You Begin page, select **Next**.

3. On the Specify Name and Location page, in the Name box, enter **SEA-W10**, and then select **Next**.

4. On the Specify Generation page, select **Generation 1** and then select **Next**.

5. On the Assign Memory page, in the Startup memory field, enter **2048** and then select **Next**.

6. On the Configure Networking page, select **Private Switch** from the drop down list, and then select **Next**.

7. On the Connect Virtual Hard Disk page, select **Use an existing virtual hard disk**, and in the Location box, enter **D:\VirtualMachines\SEA-W10.vhd**, and then select **Next**.

8. On the Completing the New Virtual Machine Wizard page, select **Finish**.

9. In Hyper-V Manager, under Virtual Machines, right-click **SEA-W10** and select **Settings**.

10. Select **Processor** and then on the Processor page, next to Number of virtual processors, change the number to **2**.

11. Select **OK** to close the Settings dialog box.

### Task 5: Create and Manage Hyper-V Checkpoints

1. In Hyper-V Manager, under Virtual Machines, select **SEA-W10** and then in the Actions pane, select **Checkpoint**.

   > A Checkpoint is created to represent the initial state of the virtual machine.

2. Under Checkpoints, select the **SEA-W10** checkpoint and then in the Actions pane, select **Rename**.

3. Rename the checkpoint to **Initial Configuration**.

4. Under Virtual Machines, select **SEA-W10** and then in the Actions pane, select **Start**. The virtual machine starts.

5. Select **Connect** to connect to SEA-W10. 

6. At the Connect to SEA-W10 dialog box, change the Display configuration to **1024 by 768** pixels, and then select **Connect**.

7. At the sign-in page, sign in as **Admin** with the password of **Pa55w.rd**. 

   > Notice that the current name of the VM is GoldImage1.

8. In the GoldImage1 VM, right-click the **Start** button, and then select **System**.

9. On the About page, scroll down and then select **Rename this PC**.

10. In the Rename your PC dialog box, enter **SEA-W10**, and then select **Next**.

11. Select **Restart now**. The virtual machine restarts.

12. After the VM restarts, select **Reconnect**, and then sign in as **Admin** with the password of **Pa55w.rd**. 

    > Notice that the name of the VM is now SEA-W10.

13. Shut down the SEA-W10 VM and then close the Virtual Machine Connection window.

14. On the Action menu, select **Checkpoint**.

15. Under Checkpoints, select the new **SEA-W10** checkpoint and then in the Actions pane, select **Rename**.

16. Rename the checkpoint to **Renamed Configuration**.

17. Under Checkpoints, select the **Initial Configuration** checkpoint and then in the Actions pane select **Apply**.

18. In the Apply Checkpoint warning, select **Apply**. 

    > Notice the that the Now indicator is placed under the Initial Configuration checkpoint to indicate that it is active.

19. Under Virtual Machines, select **SEA-W10** and then in the Actions pane, select **Start**. The virtual machine starts.

20. Select **Connect** to connect to SEA-W10. 

21. At the Connect to SEA-W10 dialog box, change the Display configuration to **1024 by 768** pixels, and then select **Connect**.

22. At the sign-in page, sign in as **Admin** with the password of **Pa55w.rd**.

    > Notice that the virtual machine is in its initial state before you renamed the computer.

23. Close the Virtual Machine Connection window.

24. Under Virtual Machines, select **SEA-W10** and then in the Actions pane, select **Revert**.

25. At the Revert Virtual Machine message, select **Revert**.

    > This will revert the VM to the Initial Configuration Checkpoint.

26. Under Checkpoints, select the **Renamed Configuration** checkpoint and then in the Actions pane select **Apply**.

27. In the Apply Checkpoint warning, select **Apply**. 

    > Notice the that the Now indicator is placed under the Renamed Configuration checkpoint to indicate that it is active.

28. Under Virtual Machines, select **SEA-W10** and then in the Actions pane, select **Start**. The virtual machine starts.

29. Select **Connect** to connect to SEA-W10. 

30. At the Connect to SEA-W10 dialog box, change the Display configuration to **1024 by 768** pixels, and then select **Connect**.

31. At the sign-in page, sign in as **Admin** with the password of **Pa55w.rd**.

    > Notice that the virtual machine is renamed to SEA-W10 which reflects the state of the Renamed Configuration Checkpoint.

32. Close the Virtual Machine Connection window.

33. Under Virtual Machines, select **SEA-W10** and then in the Actions pane, select **Revert**.

34. At the Revert Virtual Machine message, select **Revert**.

    > This will revert the VM to the Renamed Configuration Checkpoint.

35. Close Hyper-V Manager.

**Results**: After completing this exercise, you will have successfully installed Hyper-V, created a new virtual machine named SEA-W10, and managed Checkpoints.

## Exercise 2: Installing and Configuring Windows Sandbox

### Scenario

You have been asked to install the Windows Sandbox feature on SEA-CL1. You also need to ensure that the Windows Sandbox can map to a folder named D:\\Labfiles on SEA-CL1. 

### Task 1: Enable the Windows 11 Sandbox feature  

1. On SEA-CL1, select **Start**, and then select **Settings**.

2. In the **Settings** window, select **Apps**, and then select **Optional features**.

3. Scroll to the bottom of the Optional features page and then select **More Windows features**. The **Windows Features** dialog box opens.
4. In the **Windows Features** dialog box, select the check box next to **Windows Sandbox** and then select **OK**.

5. After the changes are applied, select **Restart now**.

6. After SEA-CL1 restarts, sign in as **Contoso\\Administrator** with the password of **Pa55w.rd**.

### Task 2: Start the Sandbox feature using default settings  

1. On SEA-CL1, select **Start** and then enter **Sandbox**. The **Windows Sandbox** app displays in the search results.

2. Select **Windows Sandbox**. The Windows Sandbox opens.

   > Notice that the Windows Sandbox displays as a virtual Windows 11 operating system.

3. In the Windows Sandbox, select **File Explorer**.

4. In File Explorer, select **This PC**. 

   > Notice that there is a virtual Local Disk C drive. There are no mapped folder by default.

5. Double-click **Local Disk (C:)** and review the files stored on the C drive.

6. On SEA-CL1, select **File Explorer** and browse to **D:\\Labfiles**.

7. Right-click the **Tools** folder and select **Copy**.

8. Switch to the **Windows Sandbox**, and if necessary, browse to **C:\\**.

9. In the Windows Sandbox window, right-click in the **C:\\** folder and the select **Paste**.

   > Notice that the Tools folder is copied to the sandbox VM. Windows Sandbox allows copy and paste between the host machine and the virtual machine.

10. Close the Windows Sandbox window. 

   > Take note of the Windows Sandbox warning message, which states that when the window is closed, all content will be discarded.

11. Select **OK**.

### Task 2: Start the Sandbox feature using a configuration file

1. On SEA-CL1, open File Explorer and browse to **D:\Labfiles\Mod03**.

2. Open **WindowsSandbox_Config.txt**.

3. In the HostFolder section modify the line as shown:

   ```
   <HostFolder>D:\Labfiles</HostFolder>
   ```

4. In the SandboxFolder section modify the line as shown:

   ```
   <SandboxFolder>C:\Users\WDAGUtilityAccount\Downloads</SandboxFolder>
   ```

5. Save the file as **WindowsSandbox.wsb**. You will need to change the Save as type selection to **All Files**.

6. Close Notepad.

7. If necessary, open File Explorer and browse to **D:\\Labfiles\Mod03**.

8. Double-click **WindowsSandbox.wsb**.

   > Windows Sandbox starts and automatically opens the Downloads folder in File Explorer. The content of the Downloads folder is mapped to the D:\\Labfiles folder from SEA-CL1.

9. Close the Windows Sandbox window and then select **OK**.

10. Sign out of SEA-CL1.

**Results**: After completing this exercise, you will have successfully enabled and configured Windows Sandbox.

**END OF LAB**

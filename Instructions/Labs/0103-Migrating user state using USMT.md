# Practice Lab: Migrating user state using USMT

## Summary

In this lab you will migrate user state from one computer to another using the User State Migration Tool (USMT).

### Scenario

You have deployed a new Windows 11 computer to a user named Ben. The new computer is named SEA-CL1. You need to migrate the user state from Ben's Windows 10 computer named SEA-W10-CL3 to SEA-CL1. The best way to do so is using the User State Migration Tool (USMT). The USMT install files are located at \\\\SEA-SVR2\\Labfiles\\Install\USMT. A location to store migration data has been provided at \\\\SEA-SVR2\\Labfiles\\Install\\MigrationStore.

### Task 1: Prepare the source computer

1. Sign in to **SEA-W10-CL3** as **Ben** with the password of **Pa55w.rd**.

2. Right-click the **desktop**, hover over the **New** menu item, and then select **Text Document**. Type **Demofile** and press **Enter**.

3. Double-click **Demofile.txt** and type some random text and then save the file. There should be several items on the desktop including DemoFile.txt and various desktop icons.

4. On the desktop, right-click **This PC** and then select **Manage**.

5. Expand **Local Users and Groups**, and then select **Users**. Notice the local accounts including Admin, LocalUser1 and LocalUser2.

6. Close **Computer Management** and sign out of SEA-W10-CL3.

7. Sign in to **SEA-W10-CL3** as **Contoso\\Administrator** with the password of **Pa55w.rd**.

8. Select **Start**, type **cmd** and press Enter. 

9. At the command prompt, type the following command, and then press **Enter**:

```
Net Use F: \\SEA-SVR2\Labfiles\Install\USMT /user:Contoso\Administrator Pa55w.rd
```

6. At the command prompt, type **F:**, and then press **Enter**.

7. At the command prompt, type the following, and then press **Enter**:

```
Scanstate \\SEA-SVR2\Labfiles\Install\MigrationStore\Win10 /i:migapp.xml /i:miguser.xml /o
```

_**Note**: This will take several minutes to complete._

8. Close all open windows and sign out of SEA-W10-CL3.

### Task 2: Complete the migration

1. Sign in to **SEA-CL1** as **Ben** with the password of **Pa55w.rd**.

   *Notice that the desktop icons are not visible and there is no Demofile.txt file on the desktop.*

2. Right-click **Start** and then select **Computer Management**.

3. Expand Local Users and Groups, and then select Users.

   *Notice that LocalUser1 and LocalUser2 are not listed.*

4. Sign out of SEA-CL1.

5. Sign in to **SEA-CL1** as **Contoso\Administrator** with the password of **Pa55w.rd**.

6. Select **Start** and type **cmd**. Select **Run as administrator**. 

7. At the command prompt, type the following command, and then press **Enter**:

```
   Net Use F: \\SEA-SVR2\Labfiles\Install\USMT /user:Contoso\Administrator Pa55w.rd
```

9. At the command prompt, type **F:**, and then press **Enter**.

10. At the command prompt, type the following, and then press **Enter**:

```
Loadstate \\SEA-SVR2\Labfiles\Install\MigrationStore\Win10 /i:migapp.xml /i:miguser.xml /lac:Pa55w.rd /lae /c
```

11. Type **exit** to close the command prompt.

12. Sign out of SEA-CL1.

13. Sign in to **SEA-CL1** as **Contoso\Ben** with the password of **Pa55w.rd**.

14. Right-click **Start** and then select **Computer Management**. Notice that LocalUser1 and LocalUser2 are both available.

15. Close Computer Management.

16. On the Desktop, notice the DemoFile.txt file which has been migrated from the old computer. Note: the Desktop icon settings will only apply if the client workstation is activated.

17. Sign out of SEA-CL1.


**END OF LAB**

# Practice Lab: Modifying Registry Settings Using Registry Editor

## Summary

In this lab, you use Registry Editor to modify the Windows Registry.

## Exercise 1: Modifying Registered Owner and Registered Organization Information by using the Registry Editor

### Scenario

You have noticed that the Registered Owner and Registered Organization information on SEA-CL1 is incorrect. You need to change the information to reflect Administrator as the Owner and Contoso Corp as the Organization.

### Task 1: Review the current information

1. Sign in to **SEA-CL1** as **Contoso\\Administrator** with the password: **Pa55w.rd**.

2. Select **Start** and then type **winver** and then press Enter.

   > Notice that the product is licensed to Student. You will use the Registry editor to change this to use Contoso references.

3. Select **OK** to close the **About Windows** box.

### Task 2: Use Registry Editor modify Windows settings ###

1. On SEA-CL1, select **Start** and then type **regedit**.

2. Under **Registry Editor**, select **Run as administrator**. The Registry Editor opens.

3. In the Registry Editor, expand and then select **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion**.

4. In the CurrentVersion key, double-click the **RegisteredOrganization** string value.

5. In the Edit String box, under Value data, enter **Contoso Corp** and then select **OK**.

6. In the CurrentVersion key, double-click the **RegisteredOwner** string value.

7. In the Edit String box, under Value data, enter **Administrator** and then select **OK**.

8. Close the Registry Editor.

### Task 3: Validate the Registry change

1. Select **Start** and then type **winver** and then press Enter.

   > Notice that the product is now licensed to Administrator with the organization set to Contoso Corp.

2. Select **OK** to close the **About Windows** box.

3. Sign out of SEA-CL1.

**Results**: After completing this exercise, you will have successfully changed the Registered Owner to Administrator and the Registered Organization as Contoso Corp.

**END OF LAB**

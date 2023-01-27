# Practice Lab: Managing Domain Authentication

## Summary

In this lab you will join a device to an Active Directory Domain Services (AD DS) domain.

### Scenario

You need to join SEA-WS3 to the Contoso.com AD DS domain. This will enable central management of the device and enable users to sign in using their domain credentials.

### Task 1: Join a device to an AD DS domain

1. Sign in to **SEA-WS3** as **Admin** with the password **Pa55w.rd**.

2. Select **Start**, and then select the **Settings** icon.

3. In **Settings**, select **Accounts**.

4. Select **Access work or school**.

5. On the **Access work or school** page, select **Connect**.

6. Select **Join this device to a local Active Directory domain**.

7. On the **Join a domain** prompt, type **Contoso.com** and select **Next**.

8. Type as User name **Contoso\\Administrator**, type as Password **Pa55w.rd**, and then select **OK**.

9. In the **Add an account** dialog box, under User account, enter **Ben**.

10. Under **Account type**, ensure that **Standard User** is selected and then select **Next**.

11. Select **Restart now**.

### Task 2: Verify that the device is joined properly

1. Sign in to **SEA-WS3** as **Contoso\\Ben** with the password **Pa55w.rd**. It will take several minutes for the profile to be provisioned on SEA-WS3.

2. Select **Start**, and then select the **Settings** icon.

3. In **Settings**, select **Accounts**.

4. Select **Access work or school**. Notice that the device is connected to Contoso AD domain.

5. From the taskbar, open **File Explorer**.

6. Right-click **This PC** and then select **Properties**.

7. On the **About** page, take note of the **Device name** and **Full device name**. The Domain shows **Contoso.com**.

8. Close the About and File Explorer windows.

9. Right-click the **Start** button and then select **Computer Management**.

10. Expand **Local Users and Groups**, and then select **Users**. Notice that Ben is not added to the local users list because Ben is a domain account.

11. Select the **Groups** node.

12. Double-click the **Users** group. Notice the **Contoso\\Ben** is added to the local Users group. This allows Ben to sign in to the device. Select **Cancel**.

13. Double-click the **Administrators** group. 

    > Notice that Ben is not a local administrator. However, the **Contoso\\Domain Admins** Active Directory group is added as a local administrator. Any user that is a member of the **Contoso\\Domain Admins** group will be a local administrator on this device. 

14. Select **Cancel**, and sign out of SEA-WS3.

**Results**: After completing this exercise you have successfully joined a device to an AD DS domain.

**END OF LAB**

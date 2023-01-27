# Practice Lab: Customize Windows Start and Taskbar Layouts

## Summary

In this lab you will customize and deploy a custom Windows 10 Start page layout and a custom Windows 11 taskbar layout.

## Exercise 1: Customizing the Start Layout in Windows 10

### Scenario

You need to ensure that Windows 10 devices contain the Contoso utilities apps on the Start menu. To do this, you decide to create and export a custom Start layout that only locks down the specified groups in the XML file. Users will still be able to customize other areas of the Start menu as needed.

### Task 1: Customize the Start screen

1. Sign in to **SEA-W10-CL3** as **.\\Admin** with the password **Pa55w.rd.** This signs in as the local administrator on the device.

2. Select **Start**, and right-click each tile and then select **Unpin from Start**.

3. From the Start menu, right-click each of the following apps and then select **Pin to Start:**
    - Snip & Sketch
    - Sticky Notes
    - Voice Recorder
    - Calculator
    - Alarms & Clock
    - Maps

4. In the Start screen, just above the tiles, click and select **Name group** and then replace the text with **Contoso Utilities**.

5. Close the Start menu.

### Task 2: Export the Start layout

1. On SEA-W10-CL3, right-click the Start menu and then select **Windows PowerShell (Admin)**. Select **Yes** at the User Account Control.

2. At the PowerShell window, type the following command and then press **Enter**:

```
Export-StartLayout -UseDesktopApplicationID -Path C:\Labfiles\ContosoLayout.xml
```

3. Open **File Explorer** and then browse to **C:\\Labfiles**.

4. Right-click **ContosoLayout.xml**, point to **Open with** and then select **Notepad**.

5. At the first instance of **DefaultLayoutOverride**, type the following:

```
<DefaultLayoutOverride LayoutCustomizationRestrictionType="OnlySpecifiedGroups">
```

6. Save the **ContosoLayout.xml** file and then close Notepad.

7. Close all open windows.

### Task 3: Deploy the Start layout using Local Group Policy

1. On SEA-W10-CL3, select **Start**, type **gpedit.msc** and then press **Enter**. The Local Group Policy Editor opens.

2. In the console tree, under **User Configuration**, expand **Administrative Templates**, and then select **Start Menu and Taskbar**.

3. Double-click **Start Layout**.

4. In the **Start Layout** box, select **Enabled** and under **Start Layout File** enter **C:\\Labfiles\\ContosoLayout.xml**. Click **OK** and then close the **Local Group Policy Editor**.

5. Sign out of SEA-W10-CL3.

### Task 4: Verify the Windows 10 Start layout

1. Sign in to **SEA-W10-CL3** as **Contoso\\Reda** with the password of **Pa55w.rd**.

3. Select **Start** and then take note of the Start page. The **Contoso Utilities** group displays a lock icon that specifies that the group cannot be modified.

4. In the Start menu, right-click **Calendar** and then select **Pin to Start**. Notice that you can still customize other sections of the Start page.

5. Sign out of SEA-W10-CL3.

**Results:** After completing the exercise you will have customized and deployed a custom Windows 10 Start layout.

## Exercise 2: Customizing the Start and Taskbar Layout in Windows 11

### Scenario

You have been asked to ensure that Windows 11 contains the following apps pinned to the taskbar:

- Snipping Tool
- Sticky Notes
- Weather

You will add the apps to the Windows 11 Start menu and then export the JSON file to identify the app ids. You will then modify an .XML file that has been provided to you to include the apps on the taskbar. Finally, you will deploy the taskbar xml file using Local Group Policy. 

### Task 1: Pin sample apps to the Start screen

1. Sign in to **SEA-WS1** as **.\Admin** with the password **Pa55w.rd.** This signs in as the local administrator on the device.

2. Select **Start**, and select **All apps**.

3. From the Start menu, right-click each of the following apps and then select **Pin to Start:**
   - Snipping Tool
   - Sticky Notes
   - Weather

4. Close the Start menu.


### Task 2: Export the Start layout

1. On SEA-WS1, select **Start** and then type **PowerShell**. Under Windows PowerShell, select **Run as administrator** and select **Yes** at the User Account Control.

2. At the PowerShell window, type the following command and then press **Enter**:

```
Export-StartLayout -Path C:\Labfiles\LayoutModification.json
```

3. Open **File Explorer** and then browse to **C:\\Labfiles**.

4. Right-click **LayoutModification.json**, select **Open with**, and then select **Notepad**. 

5. Select **Format** and then select **Word Wrap**.

   > Note: You can use this file to identify the packaged App ID for the apps to be pinned to the task bar. Take note of the IDs for the Snipping Tools, Sticky Notes, and Weather apps. You would also modify this file to customize the Windows 11 Start Layout, however, it must be deployed using an MDM solution such as Intune.

### Task 3: Modify a Taskbar XML file for Windows 11

1. On SEA-WS1, open **File Explorer** and then browse to **C:\\Labfiles**.

2. Right-click **TaskbarLayout.xml** and open the file with **Notepad**.

3. Under **`<taskbar:TaskbarPinList>`** add the following lines:

   ```
   <taskbar:UWA AppUserModelID="Microsoft.ScreenSketch_8wekyb3d8bbwe!App"/>
   <taskbar:UWA AppUserModelID="Microsoft.MicrosoftStickyNotes_8wekyb3d8bbwe!App"/>
   <taskbar:UWA AppUserModelID="Microsoft.BingWeather_8wekyb3d8bbwe!App"/>
   ```

4. Save the **TaskbarLayout.xml** file.

5. Your final code should look like the following:

   ```
   <?xml version="1.0" encoding="utf-8"?>
   <LayoutModificationTemplate
       xmlns="http://schemas.microsoft.com/Start/2014/LayoutModification"
       xmlns:defaultlayout="http://schemas.microsoft.com/Start/2014/FullDefaultLayout"
       xmlns:start="http://schemas.microsoft.com/Start/2014/StartLayout"
       xmlns:taskbar="http://schemas.microsoft.com/Start/2014/TaskbarLayout"
       Version="1">
     <CustomTaskbarLayoutCollection>
       <defaultlayout:TaskbarLayout>
         <taskbar:TaskbarPinList>
           <taskbar:DesktopApp DesktopApplicationID="Microsoft.Windows.Explorer" />
           <taskbar:DesktopApp DesktopApplicationLinkPath="%APPDATA%\Microsoft\Windows\Start Menu\Programs\System Tools\Command Prompt.lnk" />
           <taskbar:UWA AppUserModelID="Microsoft.ScreenSketch_8wekyb3d8bbwe!App"/>
           <taskbar:UWA AppUserModelID="Microsoft.MicrosoftStickyNotes_8wekyb3d8bbwe!App"/>
           <taskbar:UWA AppUserModelID="Microsoft.BingWeather_8wekyb3d8bbwe!App"/>
         </taskbar:TaskbarPinList>
       </defaultlayout:TaskbarLayout>
    </CustomTaskbarLayoutCollection>
   </LayoutModificationTemplate>
   ```

6. Close all open windows.

### Task 4: Deploy the Taskbar layout using Local Group Policy

1. On SEA-WS1, select **Start**, type **gpedit.msc** and then press **Enter**. The Local Group Policy Editor opens.

2. In the console tree, under **User Configuration**, expand **Administrative Templates**, and then select **Start Menu and Taskbar**.

3. Double-click **Start Layout**.

4. In the **Start Layout** box, select **Enabled** and under **Start Layout File** enter **C:\\Labfiles\\TaskBarLayout.xml**. 

5. Select the check box next to **Reapply layout at every logon**, select **OK**, and then close the **Local Group Policy Editor**.

6. Sign out of SEA-WS1.

### Task 5: Verify the Windows 11 Taskbar layout

1. Sign in to **SEA-WS1** as **Admin** with the password of **Pa55w.rd**.

2. Verify that the **Command prompt**, **Snipping Tool**, **Sticky Notes**, and the **Weather** apps are all displayed on the taskbar.

3. In the Start menu, right-click **Calendar** and then select **Pin to Start**. Notice that you can still customize other sections of the Start page.

4. Sign out of SEA-WS1.

**Results:** After completing the exercise you will have customized and deployed a custom Windows 11 Taskbar layout.

**END OF LAB**

# KB007 - Fatal Error on Startup

**Issue:** When restarting the application after a hard crash \(one where the application closes\), you receive an error:  
_A serious error occurred during startup. OpenIZ Mobile cannot continue. Please reference the following error code when seeking help :: &lt;&lt; error code &gt;&gt;_

**Applies To:** 

* OpenIZ Disconnected Client Android

**Symptoms:**

* The error mentioned in the issue section appears on splash screen
* You cannot continue loading the application

**Cause:** This error is caused because the configuration file has somehow become corrupted on the tablet data store. The device has no way of recovering from this error, and the configuration is lost. However _**the data is still in tact**_, if you want the data off the tablet, you will have to manually extract it and send the contents of the outbox manually to the server.

**Solution:**

1. Download and install the OpenIZ Disconnected Client SDK \([https://github.com/MohawkMEDIC/openizdc/releases](https://github.com/MohawkMEDIC/openizdc/releases)\)
2. Download and install the Android SDK tools \([https://developer.android.com/studio/releases/platform-tools.html](https://developer.android.com/studio/releases/platform-tools.html)\)
3. Enable developer mode on the tablet which is impacted \([https://www.androidcentral.com/how-enable-developer-settings-android-42](https://www.androidcentral.com/how-enable-developer-settings-android-42)\)
4. Extract the platform-tools-windows package to the **c:\Program Files \(x86\)\Android\android-sdk** directory ![](../.gitbook/assets/kb007-androidplatformtools.png)
5. From your start menu select **Start &gt; Open Immunize &gt; OpenIZ SDK Command Prompt**. You should see this screen: ![](../.gitbook/assets/kb007-sdk-cmd-prompt.png)
6. Change to a directory like your desktop by entering the command **cd \users{myusername}\Desktop**![](../.gitbook/assets/kb007-gotohome.png)
7. Ensure your tablet is connected via USB, if you are prompted by the device, allow the computer to access it![](../.gitbook/assets/kb007-confirmusb.png)
8. Run the following command: 1. If you are running OpenIZ Vanilla: **brainbug --pkgid=org.openiz.mobile --bkfile=mycrash.ab** 2. If you are running TImR : **brainbug --pkgid=tz.timr.mobile --bkfile=mycrash.ab**

   ![](../.gitbook/assets/kb007-runbrainbug.png)

9. You will be asked to backup. _**DO NOT ENTER A PASSWORD**_![](../.gitbook/assets/kb007-fullbackup.png)
10. If successful, brainbug will create a directory called **mycrash.ab** on your desktop.
11. Send this file to your support personnel and they will be able to extract the tablet crash files and data, If you do not have a support organization you can follow these steps: 1. Run the brainbug tool again to extract the file: **brainbug --extract=.\mycrash --bkfile=mycrash.ab** 2. In the directory .\mycrash\apps\tz.timr.mobile\f \(or org.openiz.core if using vanilla\) you will notice two folders: .config and .local, make a note of where these folders are. 3. Reset the minims configuration using **minims --reset** 4. Run the MINIMS debugging tool using **minims --ref="C:\Program Files \(x86\)\Mohawk College\OpenIZ\sdk\org.openiz.core.pak" --applet=.\** 5. Join the security realm _**to which you want to push the recovered data**_. Be sure to subscribe to the right facility. 6. Stop the mini-ims server by pressing **Enter** 7. Start the mini-ims server again \(you can press the up arrow key in windows\) 8. When asked to update press the cancel button. You will notice the mini-ims will start to do an initial sync![](../.gitbook/assets/kb007-minimsinitialsync.png) 9. Cancel this sync by pressing enter. 10. Copy the following files from your back to **%localappdata%\MINIMS**![](../.gitbook/assets/kb007-copydatabases.png) 11. Restart the mini-ims with the specified parameters from step vii.
    1. You can now access your data as though it was on the tablet \(including forcing a synchronization\).


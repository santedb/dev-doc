# KB003 - Resetting the configuration of the Windows & Linux Applications

**Issue:** You wish to reset the configuration of the Disconnected Client so you may join a different security realm, or you can subscribe to a different facility, or you wish to purge all local data from you instance of OpenIZ Disconnected Client.

**Applies To:**

* OpenIZ Disconnected Client for Windows
* OpenIZ Disconnected Client for Linux

**Solutions:** 

There are three ways to wipe the configuration of the OpenIZ disconnected client.

1. By having the application reset the environment:
   1. Close all running instances of the OpenIZ Disconnected Client
   2. Press **Start**
   3. Navigate to **Open Immunize**
   4. Click "**Reset OpenIZ Disconnected Client"**
   5. Press "**Yes**" when prompted
2. In a command window
   1. Open a command prompt window
   2. On Linux type the command : ****

      **~/usr/share/openiz/dc/bin/gtkclient --reset**

   3. On Windows type the command: 

      **"C:\Program Files \(x86\)\Mohawk College\OpenIZ\Disconnected Client\DisconnectedClient.exe --reset"**
3. By deleting the application's configuration directory
   1. Close all running instances of the OpenIZ Disconnected Client
   2. Open **Windows File Explorer**
   3. Navigate to %appdata%
   4. Delete the folder **OpenIZDC**
   5. Navigate to %localappdata%
   6. Delete the folder **OpenIZDC**
   7. ![](../.gitbook/assets/kb003-delete.png) 


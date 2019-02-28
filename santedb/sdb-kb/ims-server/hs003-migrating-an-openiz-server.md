# HS003 - Migrating An OpenIZ Server

**Purpose:** You wish to migrate a server from one hosted environment to another or to copy a configuration from one server to another in order to scale up.

**Introduction:** OpenIZ provides scale-out capabilities in which there are chained AMI configuration instances, however there are times when you wish to migrate or "spin-up" a cloned copy of the environment. This article will illustrate how to copy an existing environment to another server.

This article is not recommended for setting up a scale-out deployment \(there are better ways of doing this\), however is recommended for:

* Migrating from one hosted platform to another
* Copying a staging environment for testing

**Applies To:**

* OpenIZ IMS Server

**Steps:**

_On the source server \(the server you're copying from\):_

1. Shut down the OpenIZ host process
   * **net stop "OpenIZ Host Process"**
2. Backup the database by following the instructions listed in [HS001 - Backing up IMS server database](https://github.com/mohawkmedic/openiz-knowledge-base/tree/ebda3706cc82d21b6c3de8bb26b1dee9f2f3c392/kb011-backing-up-ims-server-database.html)
3. Navigate to **C:\Program Files \(x86\)\Mohawk College\OpenIZ**
4. Compress the folder by right clicking and selecting **Send To** &gt; **Compressed Folder** ![](../.gitbook/assets/hs003-compress.png)
5. This will create an **OpenIZ.zip** file in the **Mohawk College** folder _\(you may be asked to place the file on the desktop instead\)_   ****

_On the destination server \(the server you're copying to\):_

1. Restore the database on your target environment by following the instructions listed in [HS001 - Backing up IMS server database](https://github.com/mohawkmedic/openiz-knowledge-base/tree/ebda3706cc82d21b6c3de8bb26b1dee9f2f3c392/kb011-backing-up-ims-server-database.html)
2. Navigate to **C:\Program Files \(x86\)\Mohawk College** folder \(create it if it does not exist\)
3. Extract the **OpenIZ.zip** file into the **C:\Program Files \(x86\)\Mohawk College** folder.
4. Register the service with: **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\InstallUtil /i "C:\Program Files \(x86\)\Mohawk College\OpenIZ\openiz.exe"**
5. Start the service with **net start "OpenIZ Host Process"**


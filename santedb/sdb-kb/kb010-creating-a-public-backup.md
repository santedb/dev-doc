# KB010 - Creating A Public Backup

**Issue:** You wish to create a publicly \(non-hidden\) archive of all OpenIZ disconnected client data for use later, or for diagnostic purposes.

**WARNING:** The instructions in this knowledgebase article will result in a \(potentially\) unencrypted copy of your data being placed into a publicly accessible location on your tablet. Only follow these instructions if your organizational policy allows you to create backups.

**Applies To:**

* OpenIZ Disconnected Client Android Application
* OpenIZ Disconnected Client Windows Application
* OpenIZ Disconnected Client Linux Application

**Symptoms:**

* Not Applicable

**Cause:** Not Applicable

**Solution:**

1. From any page in the OpenIZ mobile application select the Debug -&gt; Debug Information

   ![](https://github.com/santedb/dev-doc/tree/9b45e644816a9036372ab34507ea733c8b7af72b/santedb/sdb-kb/.gitbook/assets/kb010-001.png)

2. Select the Environment tab ![](https://github.com/santedb/dev-doc/tree/9b45e644816a9036372ab34507ea733c8b7af72b/santedb/sdb-kb/.gitbook/assets/kb010-002.png)
3. In the **Datafile Information** section press "Backup Data" ![](https://github.com/santedb/dev-doc/tree/9b45e644816a9036372ab34507ea733c8b7af72b/santedb/sdb-kb/.gitbook/assets/kb010-003.png)
4. Depending on your organization's policy, you may be prompted to enter an appropriate username and password.
5. When prompted select **OK** to the warning dialog box presented to you. ![](https://github.com/santedb/dev-doc/tree/9b45e644816a9036372ab34507ea733c8b7af72b/santedb/sdb-kb/.gitbook/assets/kb010-004.png)
6. The backup process will begin, depending on the size of your data files this can take anywhere from 5 - 30 minutes.
7. When prompted restart the application ![](https://github.com/santedb/dev-doc/tree/9b45e644816a9036372ab34507ea733c8b7af72b/santedb/sdb-kb/.gitbook/assets/kb010-005.png) \_**Android 7 Users:** \_Some Samsung versions of Android 7 won't restart the application after pressing OK, this is normal. Simply restart the application manually by closing and restarting the application.
8. The backup file is located on the tablet's Documents folder. ![](https://github.com/santedb/dev-doc/tree/9b45e644816a9036372ab34507ea733c8b7af72b/santedb/sdb-kb/.gitbook/assets/kb010-006.png)


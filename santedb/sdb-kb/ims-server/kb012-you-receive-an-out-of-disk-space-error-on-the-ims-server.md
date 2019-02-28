# KB011 - You receive an "out of disk space" error on the IMS server

**Issue:** During regular operation of your OpenIZ server environment you begin to encounter synchronization issues or other errors with clients with the message "Out of disk space".

**Applies To:**

* OpenIZ Immunization Management Server

**Symptoms:**

* During synchronizations all connected tablets report a 500 error 
* The OpenIZ log files do not grow or are filled with "out of disk space" exceptions
* Using a connected web application such as the administrative portal you see an HTML error page listing "Out of disk space"

**Cause:** The cause of this issue is that the OpenIZ host server or server which you're attempting to connect to has run out of disk space.

**Solutions:** 

1. You can prune the OpenIZ log files located in C:\Program Files \(x86\)\Mohawk College\OpenIZ and named in a format similar to openiz\_20170901.log.
   1. You can delete historical log files per your retention policy
   2. Alternately you can ZIP old logs files as an archive and then delete the files.
2. Attempt to free up disk space by uninstalling programs. For more information see: [https://support.microsoft.com/en-us/help/4028054/windows-repair-or-remove-programs-in-windows-10](https://support.microsoft.com/en-us/help/4028054/windows-repair-or-remove-programs-in-windows-10)
3. You can turn down the verbosity of logs that OpenIZ produces by editing the **&lt;system.diagnostics&gt;** configuration section. This configuration section typically is structured as follows:

   ```text
     <system.diagnostics>
       <sources>
         <source name="OpenIZ.OrmLite" switchValue="Verbose">
           <listeners>
             <add name="console"/>
             <add name="rollover"/>
           </listeners>
         </source>
   ```

   1. swithValue should be set to 
      1. Verbose - Everything from the service traces is logged
      2. Information - Informational logs or more serious are logged
      3. Warning - Only errors and warnings are logged
      4. Error - Only errors are logged

4. You can procure a larger disk in a virtualized environment or install a larger hard drive in a physical environment.


# KB015 - Diagnosing Submission Errors From Mobile Device

**Issue:** The mobile device has submitted an object to the server, however the server rejects the submission with error code 422.

**Applies To:**

* OpenIZ Disconnected Client for Android
* OpenIZ Disconnected Client for Windows
* OpenIZ Disconnected Client for Linux
* Other clients connected to the IMS Server

**Symptoms:**

* When using the disconnected client application you notice a synchronization conflicts. The synchronization conflict mentions error 422 - Unprocessable Entity

  ![](../.gitbook/assets/kb014-sync-error.png)

* When contacting the HTTP service directly the service responds with HTTP code 422 and an &lt;ErrorResult&gt; message.

**Cause:** The cause can vary and the conflict itself usually indicates why the entity was rejected. In the sample provided above the error is caused by a unique constraint named ent\_rel\_unq\_enf. It is necessary to check the data that was submitted and correct the conditions under which the rejection was caused.

**Solution:**

1. Open a command prompt on your local computer \(or a computer which has the OpenIZ server tools installed\)
2. Change to `C:\Program Files (x86)\Mohawk College\OpenIZ`, or installation directory where OpenIZ server tools are installed.
3. Run the OpenIZ Administration Console `oizac` as follows:

    `oizac -r <<server address>>`

   * If you are using a different port specify it with --port=
   * If you are using TLS indicate it with --tls
   * If you have not enabled the OIZAC oauth application do so or supply an alternate with --appId and --secret

4. Provide an administrator password for your session:

   ```text
   Open Immunize Administration & Security Console v0.9.9.22162 (Fredericton CTP1)
   Copyright (C) 2015 - 2017, Mohawk College of Applied Arts and Technology
   Access denied, authentication required.
   Username:administrator
   Password:*************
   * http://XXX.XXX.XXX.XXX:8080/ami -> v.0.9.9.21739 (Fredericton CTP1)
   Ready...
   >
   ```

5. Get a list of all logs from the server by running `loglist`
6. Note the date of the log that you wish to view and use the logcat command to search the log for the error. 
   * _**Note:**_ You will want the error to be in interpreted format so we get the message that caused the error.

     ```text
     > logcat openiz_20171116 -g <search_term>
     2017-11-16T19:10:31.0000000     Error   THD#:5   Error : Npgsql.PostgresException (0x80004005): 23505: duplicate key value violates unique constraint "ent_rel_unq_enf"
     at OpenIZ.Persistence.Data.ADO.Services.Persistence.BundlePersistenceService.InsertInternal(DataContext context, Bundle data, IPrincipal principal) in C:\Users\justin\Source\Repos\openiz\OpenIZ.Persistence.Data.ADO\Services\Persistence\BundlePersistenceService.cs:line 179
     at OpenIZ.Persistence.Data.ADO.Services.AdoBasePersistenceService`1.Insert(DataContext context, TData data, IPrincipal principal) in C:\Users\justin\Source\Repos\openiz\OpenIZ.Persistence.Data.ADO\Services\AdoBasePersistenceService.cs:line 706
     at OpenIZ.Persistence.Data.ADO.Services.AdoBasePersistenceService`1.Insert(TData data, IPrincipal principal, TransactionMode mode) in C:\Users\justin\Source\Repos\openiz\OpenIZ.Persistence.Data.ADO\Services\AdoBasePersistenceService.cs:line 200 -- <?xml version="1.0"?>
     <Bundle xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://openiz.org/model">
     ```
7. If you wish to save the log file contents you can save them to a file by running:

   `logcat openiz_20171116 -g <search_term> > file.txt`

8. Correct the issue mentioned in the log file. This may require someone with developmental skills to correct a defect, or may require updating of a particular business rule. It is always recommended when developing business rules, that you add the name of the rule to the detail you return.
9. Common errors include:
   * ent\_rel\_unq\_enf - Your mobile device is attempting to relate two of the same entities in the same role. For example: Having two MOTHER relationships to the same entity.
   * Relationship \(X\) between \(Y\) &gt; \(Z\) is invalid - Your application is attempting to relate two entities in a manner which is invalid. For example, relating a Patient directly to a Place in relationship Mother \(i.e. only Persons can be a mother\).
   * fk\_xxx - Your mobile is attempting to reference an entity or act which does not exist. Usually this means that the order in which data was submitted to the server was incorrect \(for example: submitting observations to the server before the patient is submitted\).   


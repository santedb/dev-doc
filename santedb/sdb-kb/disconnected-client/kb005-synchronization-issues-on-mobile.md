# KB005 - Synchronization Issues on Mobile

**Issue:** During the course of using the disconnected client, you notice that patients re-appear on the encounter queue or that data is not being synchronized between tablets.

**Applies To:** 

* OpenIZ Disconnected Client Android Application
* OpenIZ Disconnected Client for Windows
* OpenIZ Disconnected Client for Linux

**Symptoms:**

* Patients registered on one tablet fail to appear on another device
* Vaccination appointments fail to appear on other tablets
* There are different numbers being reported in the same facility between devices
* Patients on the encounter queue disappear and/or reappear, and/or are not shown the same on more than one device
* There is an exclamation mark beside the ![](../.gitbook/assets/common-syncicon.png)icon

**Cause:** The most likely cause of any of these issues is a synchronization issue. OpenIZ disconnected client will attempt to push your changes to the server in the background during the course of your workflow. Sometimes the server will reject these changes, some of these reasons include:

* Invalid data submitted by the client
* A business rule was violated on the server 
* The connection was severed during transport of a highly compressed object
* There is some other data consistency issue such as duplicate updates, etc.

When this occurs, the tablet will place the outbound message in the deadletter queue. Because the server was not made aware of changes \(or it was but rejected them\), during the next scheduled pull, the tablet will pull down the older version of the object. This gives the appearance that your data was lost, however this is not the case. Your data is not lost, it is simply not processed yet.

**Solutions:**

* **Important:** Do no re-perform the action! This may cause further synchronization issues
* Check the sync centre to see if you have any conflicted messages![](../.gitbook/assets/kb005-syncentreconfirm.png)
* If you have a conflict you can attempt to simply resubmit them by pressing **Retry Conflicted**. 
* If the message is still rejected you can click on the **Inspect Contents** option![](../.gitbook/assets/kb005-inspect-contents.png)
* You can press the **Resolve** button to see what the conflict is![](../.gitbook/assets/kb005-resolve-issue.png)
* There are several types of errors that may occur here:
  * 500 = Server Error - The server couldn't process your message at all, it is invalid and cannot be processed until the server receives an update or data is resubmitted to correct any foreign key constraints \(see below\).
  * 422 = Business Rule Violated - There was a business rule violated on the server side, you will need to correct the conditions that caused the rule to be violated before sync can happen \(negative stock is a common cause of this\)
  * 409 = Conflict - The data that your tablet is attempting to submit is on an out dated version. This happens when concurrent updates occur.
  * 404 = Not Found - The data your tablet is trying to update is not found
  * 410 = Gone - The data your tablet was trying to update no longer exists
* You may also ignore your changes by using the "**Leave Server Version**", this will delete the outbox item.

If you notice that a 500 error is being returned by the server, and the server is logging foreign key constraints then it may be necessary to re-submit all server data.

* From the main menu select **Debug &gt; Debug Information**
* Select the **Environment** tab and locate the **Re-Submit To Server** section
* Select the date range of data you wish to re-submit, and press the **Confirm** button

  ![](../.gitbook/assets/kb005-resubmit.png)

  * Depending on your deployment, you may be required to supply an administrative password to perform the action requested.
  * The re-synchronization process may take upwards of 20-30 minutes as the tablet verifies its data integrity with the server. 


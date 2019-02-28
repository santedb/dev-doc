# KB004 - After setting up the application data appears to be missing

**Issue:** After setting up the application, and joining the security realm, and logging into the application, you notice that data is missing.

**Applies To:**

* OpenIZ Disconnected Client Android Application
* OpenIZ Disconnected Client for Windows
* OpenIZ Disconnected Client for Linux

**Symptoms:** 

* After a fresh application install, labels on the user interface are blank
* The system prevents you from logging in with "The security settings of this tablet do not allow..."
* There is a noticeable delay in login and doing data intensive actions

**Cause:** The OpenIZ Disconnected Client operates in a two-pass synchronization method, both are done in parallel and both are done asynchronously to the user interface. When you launch OpenIZ Disconnected Client it checks for data that has been modified since it last synchronized. If this is the first time you have opened the application, then all of the data on the server is new to the mobile app \(thus it must download that data you asked\).

The first thread launches first and is known as the remote sync service. This service is what is responsible for fetching data from the remote server. This service produces the message "Executing Pull Request" in the status bar of the application. This service only fetches data from the remote server and queues it for input in the inbox of the device.

The second thread is known as the queue importer service. This service listens for new published data on the inbox and then inserts the data into the primary database. This service is responsible for the "Importing Data \[30\]" message in the application status bar.

**Solution:**

* The issue of data not appearing may be a connection issue. Ensure that you are connected to the internet and that the server you are connecting to is available. 
  * If the connection is slow you should see the Executing Pull Request message periodically in your status area.
* Once data is downloaded it then needs to be imported. Depending on the speed of your device this process can be instantaneous or can take quite a long time. While this process is occurring the application will behave sluggishly and writes to the database will wait in the queue \(so if you register a patient while this process is happening, you may notice the save takes more time\)
  * This process happens in parallel with downloading. It is possible if your connection and server are fast enough that your tablet has downloaded all data but not yet imported it.
  * This only usually occurs when multiple thousands of records are downloaded at once and is not known to happen during regular use.
  * When you are running a very large clinic, the OpenIZ Disconnected Client will attempt to save server round-trips \(going back to the server for more data\), this means that some batches of inserts can be 2,500 - 5,000 records which will take some time. Because the smaller the bundle the faster the insert \(and thus the UI\). The tablet attempts to optimize in the following manner:
    * If there are more than 20,000 results the tablet will import 5,000 at a time
    * If there are more than 10,000 results, the tablet will import 2,500 at a time
    * If there are more than 5,000 results the tablet will import 1,000 at a time
    * If there are more than 1,000 results the tablet will import 500 at a time
    * Anything less than 1,000 results the tablet will import 100 at a time 


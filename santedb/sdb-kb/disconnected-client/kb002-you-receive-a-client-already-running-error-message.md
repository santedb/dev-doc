# KB002 - You receive a client already running error message

**Issue:** When you try to start the OpenIZ Disconnected Client on Windows or Linux you receive the error : "There is more than on instance of the application running. This may cause serious issues. Closing all instances of the application and restarting is recommended"

**Applies To:**

* OpenIZ Disconnected Client Windows Application
* OpenIZ Disconnected Client Linux Application

**Symptoms:**

* The application displays a window on your screen during the splash page

![](../.gitbook/assets/kb002-errordialog.png)

**Cause:** The Disconnected Client is really a miniature copy of the full OpenIZ IMS, as such it needs to open a port on your computer so that the front-end user interface can communicate with the back-end application. When more than one instance of the application is running, the second instance cannot open the port and thus the application launch fails.

You may also get this error if your computer's policy denies permission to open the port 9200 or if there is another application running on port 9200.

**Solutions:**

* Check your task bar to make sure that not more than one of the disconnected client is running. If it is close all of them.
* Press OK to close the error dialog and retry the operation.
* Try running the application as an administrator. If this works, then your user account is not permitted to open ports. Ask your system administrator which ports are permitted and update the %appdata%\OpenIZDC\openiz.config file in the ApplicationConfigurationSection the following way: &lt;setting key="openiz.mobile.core.minims.port" value="9201" /&gt;
* Check if another application is using the same port as the disconnected client \(9200\), if it is then close that application.


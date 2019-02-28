# KB006 - Disconnected Client Window is Scaled Improperly

**Issue:** When running the disconnected client in a high resolution mode \(&gt; 96 DPI\), you notice that the main contents of the window are black, don't respond properly, or don't scale properly.

**Applies To:**

* OpenIZ Disconnected Client for Windows

**Symptoms:**

* When resizing the window, the screen goes black
* When clicking on an object a portion of the screen zooms in beyond the size of the window \(hiding the contents\)
* When minimizing or maximizing the window, the internal contents of the user interface do not scale

**Cause:** The cause of this issue is the embedded Chromium instance has not been configured to be DPI aware in a way that is compatible with the host.

**Solution:**

* Right click on the disconnected client icon in your start menu and select **Open File Location** ![](../.gitbook/assets/kb006-startcommand.png)
* Right click on the OpenIZ Disconnected Client icon in the explorer window that appears![](../.gitbook/assets/kb006-explorer-rc.png)
* In the properties dialog, select **Compatibility** and then **Disable display scaling on high DPI settings**![](../.gitbook/assets/kb006-disable-scaling.png)
* Close the disconnected client and open it again


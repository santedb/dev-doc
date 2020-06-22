# When logging into the dCDR you are immediately logged back out



**Issue:** When using the SanteDB dCDR user interface from different machine \(the one not running the dCDR\) you are immediately logged out.

**Applies To:**

* SanteDB Server Disconnected Clinical Data Repository \(dCDR\)
* SanteDB Server Web Host Container \(www\)

**Symptoms:**

* You are logged in but immediately logged back out

**Cause:** This issue is caused when there is a timezone mismatch between the host running the dCDR, the central iCDR and the machine accessing the service. This is due to the dCDR sending the browser an expiration time expressed in the wrong timezone.

**Solutions:**

* Ensure that the timezone matches the dCDR server and the web browser being used to access it.
* Ensure that the time on the iCDR server and dCDR match


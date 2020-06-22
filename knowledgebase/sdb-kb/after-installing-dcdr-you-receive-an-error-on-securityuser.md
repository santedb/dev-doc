# After Installing dCDR you receive an error on SecurityUser

**Issue:** When using the SanteDB dCDR \(Gateway, Android App, etc.\) , upon login you are presented with an error indicating that a property cannot be read on SecurityUser.

**Applies To:**

* SanteDB dCDR Gateway Kelowna \(Version 2.0.22+\)
* SanteDB dCDR Android Application \(Version 2.0.22+\)
* SanteDB dCDR Windows Application  \(Version 2.0.22+\)
* SanteDB dCDR Linux Application  \(Version 2.0.22+\)

**Symptoms:**

* Upon login, you receive an error about a property of SecurityUser

**Cause:** The issue is caused because the dCDR host service is not yet completed its startup process, and has not yet loaded the specified tables and services into memory.

**Solutions:**

* Wait up to a minute and then attempt login again.


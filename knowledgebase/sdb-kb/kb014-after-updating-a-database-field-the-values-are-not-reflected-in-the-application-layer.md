# KB014 - After updating a database field the values are not reflected in the application layer

**Issue:** After updating a database field directly on the primary data source the values are not reflected on the IMSI and/or FHIR interfaces.

**Applies To:**

* OpenIZ Immunization Management Service \(IMS\)

**Symptoms:**

* When updating a database field using SQL the value is changed in the database but not reflected in applications.
* When querying a FHIR based resource the updated values do not present themselves.

**Cause:** The OpenIZ IMS uses an in-memory cache to speed up the retrieval of data from the primary data source. The two options for this are a built-in memory cache or REDIS. When you update the value directly on the database, it does not invalidate the cache data.

**Solution:**

When using the built-in memory cache:

1. Open a command prompt as Administrator
2. Restart the OpenIZ host process using the command:
   * net stop openiz
   * net start openiz
3. **Note:** Your instance of OpenIZ IMS will be unavailable during this time

When using the REDIS cache service

1. Open a command prompt as Administrator on your REDIS host server
2. Restart the REDIS process using the command
   * net stop redis
   * net start redis
3. **Note:** Your instance of OpenIZ IMS will continue to be available during this time.


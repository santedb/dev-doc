# Upgrading SanteDB iCDR with large databases

**Issue:** After installing an upgrade for a SanteDB iCDR server, the service starts never finishes, and it is logged that a database update has failed.

**Applies To:**

* SanteDB iCDR (Version 2.1.x)

**Symptoms:**

* Upon starting the Windows Service or Linux daemon you notice that the startup takes a long time
* When attempting to access the server via an API or dCDR you receive a 503 error
* In the SanteDB log file there are log entries noting:

```
SanteDB.OrmLite.Migration.SqlFeatureUtil@ [2022-01-18T09:16:05.4466863-05:00]: Could not install 20220112-01 - Npgsql.NpgsqlException (0x80004005): Exception while reading from stream ---> System.TimeoutException: Timeout during reading attempt at Npgsql.NpgsqlConnector.<g__ReadMessageLong|194_0>d.MoveNext()Cause: This rejection is caused because the ssnAuthority has not been configured for the dCDR or iCDR. 
```

**Solutions:**

1. Note the update file name in the log (example: `20220112-01`) and locate the equivalent SQL file in `$installdir$/data/sql/updates/20220112-PSQL.sql` (note: Firebird database have `-FBSQL` as their suffix)
2. Open a connection to the database using a client tool (like PGAdmin, DBeaver, etc.)
3. Run the update file manually
4. Kill the SanteDB host process
5. Restart the SanteDB iCDR host process


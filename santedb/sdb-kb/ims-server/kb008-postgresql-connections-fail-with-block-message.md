# KB008 - PostgreSQL connections fail with block message

**Issue:** During heavy operation, or when two IMS servers are accessing one PostgreSQL server, you receive an error message related to the PostgreSQL server being unavailable or rejecting your connection attempt.

**Applies To:**

* OpenIZ Immunization Management System

**Symptoms:**

* Synchronizations or applications no longer work or are very slow
* You find the log one of the following errors in your log files multiple times
  * Npgsql.PostgresException \(0x80004005\): 53300: remaining connection slots are reserved for non-replication superuser connections 
  * Error on IMSI WCF Pipeline: Npgsql.NpgsqlException \(0x80004005\): Exception while reading from stream ---&gt; System.IO.IOException: Unable to read data from the transport connection: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond
* You are unable to connect to the server via administration tools

**Cause:** The cause lies with an overflow of connections against the PostgreSQL server. This is very common when hosting the IMS on AWS or other hosted providers which limit the number of concurrent connections to the server.

**Solutions:**

* You can increase the number of maximum connections allowed to the database. This can be done by upgrading the AWS RDS instance, or \(if not hosting on AWS\) increasing the maximum connections settings in postgres.config
* You can force-disconnect all clients on your database by running the following command 

```sql
select pg_terminate_backend(pid)
from pg_stat_activity
where datname = 'yourdatabasename'
```

* You can disable multi-threaded fetches from the data store with the following setting on your &lt;connectionManager&gt; element

```markup
<openiz.persistence.data.ado>
     <connectionManager stm="true" 
          maxRequests="4"
          />
```

* You can reduce the number of IMS instances contacting the particular database server
* You can scale-out the database to introduce read-only nodes, thus reducing the load on the primary data server. For this see how to setup synchronous replication in PostgreSQL.


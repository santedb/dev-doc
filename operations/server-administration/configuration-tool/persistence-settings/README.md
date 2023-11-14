# Persistence Settings

The persistence settings group in the configuration tool contains the control panels for SanteDB's data persistence services, and operations related to the storage, archiving and referencing of data.

## Common Settings

The persistence settings typically share a common configuration structure as illustrated below.

![](<../../../../.gitbook/assets/image (419) (1) (1) (3).png>)

| Option                       | Description                                                                                                                                                                                                          | Example                                              |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| Read/Write Connection String | Identifies the read/write connection string to use. This connection should be to the server which can accept read requests and write requests. In a scaled solution this is the primary or master database node.     | See: [Database Connections](database-connections.md) |
| Read-Only Connection String  | Identifies the connection / pool to use for all query and read operations. No write operations are sent to this connection string. This can be a pool of replicas from which data is queried in the SanteDB service. | See: [Database Connections](database-connections.md) |
| Data Provider                | The data provider to use for connecting and converting physical object models to SQL.                                                                                                                                |                                                      |
| Trace SQL                    | True if the SQL statements going to the database server should be logged into the diagnostics source.                                                                                                                |                                                      |

## ADO.NET Data Persistence Service

The ADO.NET data persistence service as well as the archiving service share a common configuration options.&#x20;

![](<../../../../.gitbook/assets/image (420) (1) (1) (1).png>)

| Option                          | Description                                                                                                                                                                                                                                                          | Example       |
| ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| Auto-Updating Existing Resource | When true, the persistence layer will automatically treat a request to create an existing resource as an update. This behavior indicates that `Insert(123)` followed by `Insert(123)` does not cause an error, rather the second `Insert` is treated as an update.   | Boolean       |
| Auto-Insert Child Objects       | When true, the persistence layer will automatically insert child objects into the database. When false, an attempt to insert an object where the child object (for example the target of an EntityRelationship) does not exist will result in a key not found error. | Boolean       |
| Data Corrections                | If using an older version of the OpenIZ database, the automatic corrections you want applied to the data being sent and persisted.                                                                                                                                   | String List   |
| Allowed Resources               | If the administrator wishes to bar the storage of specific types of resources in the database, they can set one or more resources which should be restricted on the persistence layer.                                                                               | Resource List |
| MaxPageSize                     | The maximum number of results that can be returned in a single page of a query. For performance reasons the default of this is 10,000 results in a single query result set.                                                                                          | Number        |
| Use Approx Totals               | When true, the system will use an approximate total which is sufficient to trigger a "next page" indicator on user interfaces and synchronizations. If false, the system will count all the results in the result set and then return the results.                   | Boolean       |
| Single Threaded Fetch           | When true, the system will not use PLINQ to fetch results from the database, rather it will use a regular LINQ enumerator                                                                                                                                            | Boolean       |
| Request Throttling              | The maximum number of database requests to allow on the iCDR server. 0 indicates that no limit is set.                                                                                                                                                               | Number        |
| Prepare SQL Queries             | When true, the ORM library will execute a `Prepare()` operation on queries and will re-use prepared queries and query plans. This can be beneficial on queries which are commonly reused.                                                                            | Boolean       |

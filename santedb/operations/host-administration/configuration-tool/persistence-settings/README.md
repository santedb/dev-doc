# Persistence Settings

The persistence settings group in the configuration tool contains the control panels for SanteDB's data persistence services, and operations related to the storage, archiving and referencing of data.

The persistence settings typically share a common configuration structure as illustrated below.

![](<../../../../../.gitbook/assets/image (426).png>)

| Option                       | Description                                                                                                                                                                                                          | Example                                              |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| Read/Write Connection String | Identifies the read/write connection string to use. This connection should be to the server which can accept read requests and write requests. In a scaled solution this is the primary or master database node.     | See: [Database Connections](database-connections.md) |
| Read-Only Connection String  | Identifies the connection / pool to use for all query and read operations. No write operations are sent to this connection string. This can be a pool of replicas from which data is queried in the SanteDB service. | See: [Database Connections](database-connections.md) |
| Data Provider                | The data provider to use for connecting and converting physical object models to SQL.                                                                                                                                |                                                      |
| Trace SQL                    | True if the SQL statements going to the database server should be logged into the diagnostics source.                                                                                                                |                                                      |

# Production Installation Notes

When you install SanteDB iCDR server or any of the SanteDB solutions (like SanteMPI or SanteIMS), the default installer uses a "quick start" configuration. These configurations are intended to get implementers up and running quickly, however there are several caveats to defaults.&#x20;

## Dispatcher Queue

The dispatcher queue service is used to reliably store an outbound message to a reliable place so:

* In-process actions aren't slowed by the response time of an external system,
* Messages are delivered in a reliable fashion

### File-Based Dispatcher Queue&#x20;

The default dispatcher queue used by SanteDB on all installations is a file-system based queue. This allows for a simplistic reliable messaging management where each outbound request or queue request is written and read as a file on the file system. This service is useful when:

* The server will have a low volume of messages sent to it
* The server will have low latency connections to any subscribed services

The file-based dispatcher queue, however can severely impact performance on high volume SanteDB iCDR services.&#x20;

{% hint style="info" %}
It is not recommended to use the File-Based dispatcher queue in a production environment.
{% endhint %}

### Microsoft Message Queue (MSMQ)

The MSMQ dispatcher allows SanteDB iCDR to connect to a Microsoft Message Queue server. This service allows SanteDB iCDR servers to queue messages to the MSMQ service on a local machine (`.\\$Private`) or on a remote machine (with appropriate configuration).  MSMQ is suitable when:

* The server will have a moderate to high level of server traffic sent it
* The server may have longer-lasting connections or unreliable connection to remote machines (i.e. queue lifetime may be longer)
* There is no need to failover or scaling queue functions.

For more information about installing Microsoft Message Queue consult the [Microsoft Documentation ](https://docs.microsoft.com/en-us/dotnet/framework/wcf/samples/installing-message-queuing-msmq). See the [#microsoft-messaging-queue](../../../operations/server-administration/configuration-tool/system-settings.md#microsoft-messaging-queue "mention") topic for a description of enabling MSMQ on SanteDB iCDR.

### RabbitMQ

The RabbitMQ plugin is currently in development. RabbitMQ will allow users of SanteDB iCDR on Linux, Docker or Windows to connect SanteDB to a RabbitMQ server.

## Database Infrastructure

SanteDB iCDR server generates large volumes of audits. Depending on the load under which the server is running, it may be beneficial to split the logical roles of the SanteDB databases. In general, SanteDB databases should be split by role, and where possible, these databases should be running on different physical hardware (in virtual machines, however on different disk infrastructure).

| Audit Database                  | High write volumes , low read volumes |
| ------------------------------- | ------------------------------------- |
| Primary / Clinical Database     | High write volumes, high read volumes |
| Pub-Sub Subscription Management | High read volumes, low write volumes  |

### Pooling and Auto-Prepare

When running SanteDB iCDR in a production context, it is recommended that implementers enable pooling and tune their connection settings to match their environment. For example, the deployment of PostgreSQL may be modified to enable larger connection pool allowances (concurrent connections). These settings are highly dependent on the context in which SanteDB is operating (how many clients, load, traffic patterns, etc.).

| Pooling            | Enables connection pooling                                                                                                                                                            | Should be set to `true` in production environments                                                                                      |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| Minimum Pool Size  | Sets the minimum active connections to keep in the connection pool.                                                                                                                   | Should be set to a reasonable number to support bursts in traffic (for example: `10`)                                                   |
| Maximum Pool Size  | Sets the maximum number of active connections to allow to connection pool. After the connection pool is exceeded, connections will need to wait for a connection to become available. | Should be set based on the number of concurrent requests expected (example: `100` is a good number for up to 10 concurrent connections) |
| Max Auto Prepare   | Sets the number of statements that will be automatically prepared. Statement prepare commands are useful in that the database server needn't re-plan similar queries.                 |                                                                                                                                         |
| ConnectionLifetime | The maximum lifetime of a connection in the connection pool. This is recommended for load balancing as it forces new connections to another server.                                   |                                                                                                                                         |

### PostgreSQL Failover

Implementers are encouraged to run their PostgreSQL infrastructure in failover clusters and (if possible) in a scaled deployment.

{% hint style="info" %}
Implementers should consult the PostgreSQL failover clustering tutorial on EnterpriseDB to setup a failover environment. [https://www.enterprisedb.com/postgres-tutorials/postgresql-replication-and-automatic-failover-tutorial](https://www.enterprisedb.com/postgres-tutorials/postgresql-replication-and-automatic-failover-tutorial)
{% endhint %}

To configure SanteDB iCDR to use a PostgreSQL failover, you should modify the connection string parameter to be a list of server addresses separate by a comma, for example:

```xml
<add name="main" 
    value="server=hotserver:5432,coldfailover:5432; database=x; user id=x; password=x;pooling=true; "
    provider="Npgsql" />
```

### PostgreSQL Load Balancing

Implementers can use PostgreSQL Streaming Replication (unidirectional, real-time replication) or asynchronous replication to enhance performance. In SanteDB's configuration file, it is possible to specify a `readonlyConnectionString` and a `readWriterConnectionString`. These two connection strings should point at pools of read/write primary addresses and a pool of read-only secondary addresses.

Assuming that a scaled SanteDB iCDR deployment has four PostgreSQL servers:

| 192.168.0.100 | Primary (Hot)   |
| ------------- | --------------- |
| 192.168.0.101 | Failover (Cold) |
| 192.168.0.102 | Replica (Hot)   |
| 192.168.0.103 | Replica (Hot)   |

A configuration may be set as:

```xml
<section xsi:type="AdoPersistenceConfigurationSection"
           readWriteConnectionString="READWRITE"
           readOnlyConnectionString="READONLY"
           ... >
<section xsi:type="DataConfigurationSection">
  <connectionStrings>
    <add name="READWRITE" value="server=192.168.0.100,192.168.0.101; Target Session Attributes=primary ..." provider="Npgsql" />
    <add name="READONLY" value="server=192.168.0.102,192.168.0.103; Target Session Attributes=prefer-standby;Load Balance Hosts=true" provider="Npgsql" />
  </connectionStrings>
</section>
```

## Tune Unused Services

The default installation of several SanteDB solutions will enable services which may not be required in every jurisdiction. Disabling these services may drastically increase throughput of the solution.

### Privacy Enforcement Service

You can disable the `DataPrivacyFilterService` (in Docker `DATA_POLICY` feature) to increase query and write performance. This service attaches to all disclosure pathways in the SanteDB server and applies appropriate masking and filtering based on user roles.&#x20;

Disabling this service will result in the disclosure of all data (regardless of policy tagging), however does reduce the overhead of applying policies.&#x20;

Disable this service when:

* Your deployment uses an upstream privacy control solution (i.e. there is an intermediary which applies policies)
* Your deployment has no need for special data protection policies

### JavaScript Business Rules

The JavaScript business rules engine is a feature which allows SanteDB applets to subscribe to events on the dCDR or iCDR server. The applets can define business rules in ECMA5 script (for more information see: [business-rules.md](../../../developers/extending-santesuite/extending-santedb/applets/business-rules.md "mention")).

Disabling this service can save 10-20% of the execution time for write and update transactions, and about 10% of the execution time of queries. This is because it saves the iCDR server from serializing and parsing JSON and interacting with the single-threaded JavaScript execution (although, SanteDB creates a pool of single-threaded JavaScript execution engines).

Disable this service when:

* Your implementation is not using JavaScript business rules or you have ported your business rules to C#
* You are only using the dCDR to connect to the iCDR (no other interfaces are enabled) and your dCDR instances will be running the JavaScript business rules.

### Data Quality Validation Service

You can also disable the default data quality service. By default, SanteDB iCDR allows implementers to specify a series of data quality rules which are applied on all data entering the iCDR. The data quality validation service executes these rules and tags/flags failures (rather than rejecting the request entirely).&#x20;

Disabling this service means that no data quality validation is performed. This may be suitable if:

* Your user interface already ensures that these rules are followed
* The solution has C# logic or a scheduled job which can run these rules in the background

{% hint style="info" %}
The SanteDB team is implementing a background method for running data quality rules.
{% endhint %}

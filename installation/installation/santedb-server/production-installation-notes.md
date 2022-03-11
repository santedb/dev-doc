# Post Deployment Tuning

When you install SanteDB iCDR server or any of the SanteDB solutions (like SanteMPI or SanteIMS), the default installer uses a "quick start" configuration. These configurations are intended to get implementers up and running quickly, however the default options will not result in optimal performance. A common source of system performance issues is interfaces to external systems. To decouple SanteDB responsiveness from external systems and obtain the best possible performance, SanteDB makes use of message queue services to manage outbound messages. The default message queue installation automatically supports all operating systems, however further optimization is possible by directing SanteDB to make use of third party tools. Please read below to learn more about optimizations that are available.     &#x20;

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

### Windows Server Optimization - Microsoft Message Queue (MSMQ)

In installations where Microsoft Windows Server is used exclusively as the underlying operating system for SanteDB, it is recommended that Microsoft Message Queue (MSMQ) is used for message queueing services. MSMQ offers extremely high performance and reliable message delivery but is an operating system level service provided by Microsoft Windows Server. When deploying SanteDB in non-Windows or mixed operating system environments, please see the following section on RabbitMQ.&#x20;

In a MSMQ deployment, the MSMQ _dispatcher_ allows SanteDB iCDR to connect to a Microsoft Message Queue _server_. This service allows SanteDB iCDR servers to queue messages to the MSMQ service on a local machine (`.\\$Private`) or on a remote machine (with appropriate configuration).  MSMQ is suitable when:

* The server will have a moderate to high level of server traffic sent it
* The server may have longer-lasting connections or unreliable connection to remote machines (i.e. queue lifetime may be longer)
* There is no need to failover or scaling queue functions.

For more information about installing Microsoft Message Queue consult the [Microsoft Documentation ](https://docs.microsoft.com/en-us/dotnet/framework/wcf/samples/installing-message-queuing-msmq). See the [#microsoft-messaging-queue](../../../operations/server-administration/configuration-tool/system-settings.md#microsoft-messaging-queue "mention") topic for a description of enabling MSMQ on SanteDB iCDR.

### RabbitMQ

RabbitMQ is the most widely deployed open source message broker. For SanteDB deloyments that use Linux, Docker or a mixture of Linux, Docker and Windows Server as their underlying operating environment, RabbitMQ is the recommended high-performance message passing service. RabbitMQ can also be used in the Windows Server environment if desired. &#x20;

The RabbitMQ plugin is still currently under development with a targeted release date of Q1 2022. RabbitMQ will allow users of SanteDB iCDR on Linux, Docker or Windows to connect SanteDB to a RabbitMQ server to dramatically improve the performance of external interfaces.&#x20;

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

### Partitioning Tables

SanteDB provides opportunities to partition large tables when deployed on PostgreSQL. Depending on the type of data and the volumes of data being stored, partitioning can allow PostgreSQL to break apart large tables into smaller tables based on attributes within the table.

In SanteDB there are several tables which are candidates for partitioning, and how an implementer partitions these tables will depend on their use case for SanteDB.

| Table                                                         | Partition List                                                               | Notes                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><code>ent_vrsn_tbl</code><br><code>act_vrsn_tbl</code></p> | `cls_cd_id` (note: in 2.1.x and 2.2.x the partition should be on `ent_tbl`). | Partitioning by entity classification codes is useful when you're using the MDM or storing a large number of varied entities (i.e. places, materials, etc.) The partitions implementers define will depend on the use case for the SanteDB deployment, for example: MDM for an MPI it may be useful to create a partition for MDM-Master, Patient, Person, Organization and everything else.                                                                     |
| <p><code>ent_rel_tbl</code><br><code>act_rel_tbl</code></p>   |  `rel_typ_cd_id`                                                             | Partitioning by entity relationship classification codes is useful when storing large volumes of relationships (SanteIMS and SanteMPI are good candidates). The partitions created will depend on the use case of the deployment, for example, when using SanteMPI it may be useful to partition this table based on MDM relationship types (MDM-Master, MDM-Candidate, MDM-RecordOfTruth) , personal relationship types (Mother, Father, etc.), and all others. |
| `act_ptcpt_tbl`                                               | `rol_cd_id`                                                                  | Partitioning act participations is useful when your SanteDB deployment will store large volumes of participation information (entity to act relationships). Partitioning this table is useful for IMS deployments or deployments of SanteDB with large clinical datasets.                                                                                                                                                                                        |

An example of partitioning the `ent_vrsn_tbl` and `act_vrsn_tbl` is provided in the file `ZZ-Partition-PSQL11.sql` (for PostgreSQL 11+) and `ZZ-Partition-PSQL10.sql` (for PostgreSQL 10)

### Removing Semantic Validation

By default SanteDB iCDR's database (on PostgreSQL and Firebird) has a series of check constraints which are used for validating the codification of fields and relationships. These checks are implemented in the database to prevent rogue SQL scripts for assigning, for example, a GenderConcept to a Status (i.e. the status of an Entity cannot be `Male`) and to prevent non-sensical relationships (i.e. adding an `Uncle` to `Good Health Hospital` ).&#x20;

Depending on the resources available, and the maturity of your deployment (i.e. are all new enhancements tested prior to rollout), the size of the deployment (i.e. resources for the database server), and processes (i.e. can external objects add new data to the iCDR) you may wish to disable these checks.&#x20;

To disable these checks:

```
ALTER TABLE public.ent_rel_tbl DISABLE TRIGGER ent_rel_tbl_vrfy; -- RELATIONSHIP VALIDATION

-- For Version 2.0.x, 2.1.x, 2.2.x
DROP FUNCTION ck_is_cd_set_mem CASCADE; -- DROPS SEMANTIC FIELD VALIDATION
-- For Version 2.3.x
DROP FUNCTION ck_is_cd_set_mem_with_null CASCADE; -- DROPS SEMANTIC FIELD VALIDATION
DROP FUNCTION ck_is_cd_set_mem CASCADE; -- DROPS SEMANTIC FIELD VALIDATION
```

### Encryption at Rest

The contents of the PostgreSQL database are, by default, not encrypted. If your context requires encryption at rest, you may do so by placing sensitive data in SanteDB onto a tablespace which is stored on an encrypted volume.

To do this:

1. Create a data volume which will be used to store the PostgreSQL database
2. Format the new volume
3. Encrypt the new volume using either [BitLocker ](https://docs.microsoft.com/en-us/windows/security/information-protection/bitlocker/bitlocker-basic-deployment)(on Microsoft Windows) or [LUKS ](https://www.redhat.com/sysadmin/disk-encryption-luks)(on Linux)
4. Mount the new volume (in Windows as a drive letter, or on Linux as a mount point)
5. Create a new tablespace in PostgreSQL which is on the protected volume (`CREATE TABLESPACE encrypted LOCATION '/var/......';`)
6. Move tables which require encryption (or the entire database) to the new tablespace. For example, to place identifier values on the encrypted table space `ALTER TABLE ent_id_tbl SET TABLESPACE encrypted;`)

{% hint style="info" %}
If you use disk encryption, you may wish to do so in the Virtual Machine instance which will protect the disk contents even when the VHD is moved by the host (and in backups). If the disk encryption is turned on the host, then the VHD data will be decrypted during backups or copying of the VHD files (however, VM disk encryption may impact dynamic/hot migration VMs in a clustered environment using technologist like VMotion). Determine the best method of encrypting your data based on the technology used locally in your deployment.
{% endhint %}

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

## Distributed / Clustered Environments

SanteDB iCDR can be deployed in a distributed nature, however there are some caveats to choosing this type of deployment which will impact the rollout of SanteDB.

### Caching

The caching environment in a clustered SanteDB iCDR application server environment should be configured such that.

|                         | Single Server       | Clustered                                  |
| ----------------------- | ------------------- | ------------------------------------------ |
| Data Cache              | In-Process or REDIS | REDIS recommended (In-Process inefficient) |
| Ad-Hoc Cache            | In-Process or REDIS | REDIS required                             |
| Query Persistence Cache | In-Process or REDIS | REDIS required                             |

### Service Configuration

Currently, in SanteDB iCDR - the service hosts use a local configuration file to start up and read application configuration settings (the exception to this is the Docker host which uses environment variables for settings). If clustering your application servers, it is important that these files reflect the role of the application server in the SanteDB cluster, and that each configuration file in the cluster is synchronized based on that role.&#x20;

For example, a clustered environment may be deployed as:

| Logical Role           | Servers                                                                                | Configuration                                                                                                                                                         |
| ---------------------- | -------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Database Server        | <p>master.db.santedb.org<br>secondary1.db.santedb.org<br>secondary2.db.santedb.org</p> | Standard PostgreSQL streaming replication                                                                                                                             |
| REDIS cache server     | cache.santedb.org                                                                      | Memory-Only REDIS                                                                                                                                                     |
| AMI APP Server         | ami.santedb.org                                                                        | <ul><li>Job Schedules</li><li>Applet files</li><li>ADO.NET match configuration source</li></ul>                                                                       |
| HDSI + BIS APP Servers | <p>hdsi1.santedb.org<br>hdsi2.santedb.org</p>                                          | <ul><li>ADO.NET match configuration source</li><li>ADO.NET Data Quality </li><li>ADO.NET Clinical Protocol Repository</li><li>AMI applet repository source.</li></ul> |

### Match Configuration Service

At the time of writing, only file-system based match configuration services are supported by SanteDB iCDR. Since a distributed application environment would yield varying results as clients bounce between application servers, it using SanteDB in a distributed application server environment, it is recommended that the match configuration service be set to a UNC network share (where each application server can read configuration data from a common directory).

{% hint style="info" %}
The SanteDB community is working on a solution for match configurations which uses database configurations to ease clustering.
{% endhint %}

###

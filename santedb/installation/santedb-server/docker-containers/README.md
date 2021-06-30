# Docker Containers

SanteDB provides several docker containers for SanteDB solutions and services. The docker containers are structured as illustrated.

![](../../../../.gitbook/assets/image%20%28198%29.png)

The docker containers all use the mono:latest as their root container.

* santedb\_icdr: The generic SanteDB iCDR project running as a docker container with FHIR, HL7, caching, PostgreSQL database support, and everything needed to get the iCDR running quickly.
* santedb\_mpi: The generic iCDR project with the SanteGuard and SanteMPI plugins enabled.
* santedb\_dcdr: The disconnected dCDR project

## Configuring the Docker Containers

### Enabling or Disabling Features

The docker containers are configured using environment variables. Features can be turned on/off using the environment variable SDB\_FEATURE environment variable, for example, to enable the core features and ATNA audit shipping:

```text
SDB_FEATURE=AUDIT_SHIPPING;ADO;AUDIT_REPO
```

The features which are available for the default SanteDB docker container are:

### Database Connections

The location of your PostgreSQL server, and the database to use for the container can be specified with the connection string environment variables: 

```text
SDB_DB_PSQL="server=location;user=user;password=password;database=db"
SDB_DB_PSQL_PROVIDER=Npgsql
SDB_DB_AUDIT=" ... "
```

If you are using plugins which require additional named configuration parameters, prefix the configuration with `SDB_DB_XXX` where XXX is the ID of the connection string the plugin is expecting.

### Configuring Components

Components within SanteDB iCDR can be configured using environment variables. The syntax of these environment variables is `SDB_FEATURE_SETTING` , for example, the CACHE feature is configured as:

```bash
SDB_FEATURE=CORE_CDR,CACHE
# Caching Mode = REDIS  | LOCAL
SDB_CACHE_MODE=REDIS
# Pointer to redis server
SDB_CACHE_REDIS_SERVER=sdb-redis:6379
# Expire cache entries after X timestamp
SDB_CACHE_EXPIRE=PT1H
```

### Minimal Application 

You can compose a minimal application with either the SanteDB-ICDR or SanteMPI instance using a docker-compose.yml file as shown.

```yaml
version: "3.3"

services:
  db:
    image: postgres
    container_name: sdb-postgres
    ports:
      - "5432:5432"
    environment:
      POSTGRES_USER: santedb
      POSTGRES_PASSWORD: SanteDB123
    restart: always

  santedb:
    image: santesuite/santedb-icdr:2.1.3
    container_name: santedb-icdr
    environment:
      - SDB_FEATURE=LOG;DATA_POLICY;AUDIT_REPO;ADO;PUBSUB_ADO;RAMCACHE;SEC;SWAGGER;OPENID;FHIR;HL7;HDSI;AMI;BIS
      - SDB_DB_MAIN=server=sdb-postgres;port=5432; database=santedb; user id=santedb; password=SanteDB123; pooling=true; MinPoolSize=5; MaxPoolSize=15; Timeout=60;
      - SDB_DB_AUDIT=server=sdb-postgres;port=5432; database=auditdb; user id=santedb; password=SanteDB123; pooling=true; MinPoolSize=5; MaxPoolSize=15; Timeout=60;
      - SDB_DB_MAIN_PROVIDER=Npgsql
      - SDB_DB_AUDIT_PROVIDER=Npgsql
      - SDB_DELAY_START=1000
    ports:
      - "8080:8080"
      - "2100:2100"
    depends_on:
      - db
    restart: always
```

### Volumes

Some directories in the docker image are useful for development purposes. For example, you can configure a volume which exposes a common configuration file set, or common applets. The volumes which can be expose \(and their directories\) can be done via:

```yaml
services:

   # ... truncated for space ...
   
   santedb:
      image: santesuite/santedb-icdr:2.1.3
      # .. truncated ...
      volumes:
         - santedb-data:/santedb/data

volumes:
   santedb-data:
```

The volumes which are of use for exposing to the host docker environment are:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Path</th>
      <th style="text-align:left">Use</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">/santedb/data</td>
      <td style="text-align:left">
        <p>Used for seeding data into the SanteDB instance. For example</p>
        <p>if you have a development environment where you&apos;d like the same data</p>
        <p>seeded into the database on startup you can use this option.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">/santedb/config</td>
      <td style="text-align:left">
        <p>Used for direct access to the configuration files. You should use this
          option</p>
        <p>if the environment variables for the docker instance are too restrictive.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">/santedb/applets</td>
      <td style="text-align:left">
        <p>Used for loading applet files which contain user interfaces, BI reports,</p>
        <p>business rules, CDSS rules, etc. These applets should be digitally signed</p>
        <p>PAK files.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">/santedb/match</td>
      <td style="text-align:left">
        <p>Stores the match configuration files for the SanteDB matching engine.
          These</p>
        <p>match configuration files control the weight, blocking, and classification
          subsystem</p>
        <p>for the default match algorithm.</p>
      </td>
    </tr>
  </tbody>
</table>

## Advanced Configurations

You can import additional configuration files and/or use the XML configuration subsystem by creating a new container which is based off the `santedb-icdr` docker image and including additional configuration files. To do this, collect your configuration file as `myconfig.xml` in a directory and create a new Dockerfile which starts using this as configuration file:

```elixir
FROM santedb-icdr:latest
RUN mkdir /myproject
COPY myconfig.xml /myproject/myconfig.xml
WORKDIR /santedb
EXPOSE 2100/tcp
EXPOSE 8080/tcp
CMD ["mono","/santedb/SanteDB.Docker.Server.exe","/myproject/myconfig.xml"]
```

### Adding Sample Data

See the Adding Sample Data article for methods of seeding sample data into SanteMPI.

### Packaging Custom Business Rules

You can package [business rules](../../../extending-santedb/applets/business-rules.md), [business intelligence](../../../extending-santedb/applets/business-intelligence-bi-assets/), and other [asset files](../../../extending-santedb/applets/assets/) into your docker container by simply composing them into a PAK file and including them in the /santedb/applets/ directory.

```markup
FROM santedb-icdr:latest
COPY custom.pak /santedb/applets/custom.pak
```

Upon load, the SanteDB iCDR server will load your package files and will load any business rules files required.

## Other Containers

The `santedb-icdr` container is the generic ICDR instance for SanteDB, however SanteSuite provides other containers which are pre-configured with the necessary plugins for those functions:

* `santedb-mpi` : SanteDB + SanteMPI plugins pre-deployed
* `santedb-guard` : SanteDB + SanteGuard plugins pre-deployed

### SanteMPI Application

In order to run a minimal SanteMPI application, you can exchange `santedb-icdr` with the `santedb-mpi` image, and apply the appropriate service configuration.

```yaml
version: "3.3"

services:
  db:
    image: postgres
    container_name: sdb-postgres
    ports:
      - "5432:5432"
    environment:
      POSTGRES_USER: santedb
      POSTGRES_PASSWORD: SanteDB123
    restart: always

  santedb:
    image: santesuite/santedb-mpi:latest
    container_name: santedb-mpi
    environment:
      - SDB_FEATURE=LOG;DATA_POLICY;AUDIT_REPO;ADO;PUBSUB_ADO;RAMCACHE;SEC;SWAGGER;OPENID;FHIR;HL7;HDSI;AMI;BIS;MDM;MATCHING;IHE_PIXM;IHE_PDQM;IHE_PMIR
      - SDB_MATCHING_MODE=WEIGHTED
      - SDB_MDM_RESOURCE=Patient=org.santedb.matching.patient.default
      - SDB_MDM_AUTO_MERGE=false
      - SDB_DB_MAIN=server=sdb-postgres;port=5432; database=santedb; user id=santedb; password=SanteDB123; pooling=true; MinPoolSize=5; MaxPoolSize=15; Timeout=60;
      - SDB_DB_AUDIT=server=sdb-postgres;port=5432; database=auditdb; user id=santedb; password=SanteDB123; pooling=true; MinPoolSize=5; MaxPoolSize=15; Timeout=60;
      - SDB_DB_MAIN_PROVIDER=Npgsql
      - SDB_DB_AUDIT_PROVIDER=Npgsql
      - SDB_DATA_POLICY_ACTION=HIDE
      - SDB_DELAY_START=5000
    ports:
      - "8080:8080"
      - "2100:2100"
    depends_on:
      - db
    restart: always
```




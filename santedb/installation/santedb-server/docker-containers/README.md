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

You can quickly add test/sample data by copying [dataset files](../../../extending-santedb/applets/distributing-data.md) into the `/santedb/data` directory of the docker container. These dataset files can be generated from the `sdbac` command prompt with the `cdr.query` command to produce dataset files.

For example, to initialize an MPI with an identity domain, and an organization with a custom policy, for a particular use case, create a new dataset file containing the identity domain, organization and custom policy:

```markup
<?xml version="1.0"?>
<dataset id="Elbonia Identity Domains" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://santedb.org/data">
  <!-- National Health Identifier -->
  <insert skipIfError="false" skipIfExists="true">
    <AssigningAuthority xmlns="http://santedb.org/model">
      <name>Elbonia</name>
      <domainName>MOH_NHID</domainName>
      <oid>1.3.6.1.4.1.52820.5.0.1.1.1</oid>
      <url>http://mpi.moh.gov.elb/identity/moh/nhid</url>
      <isUnique>true</isUnique>
      <validation>^\d{12}$</validation>
      <scope>bacd9c6f-3fa9-481e-9636-37457962804d</scope>
    </AssigningAuthority>
  </insert>
  <update insertIfNotExists="true">
    <Organization xmlns="http://santedb.org/model">
      <id>fae7b5fb-ea49-4460-9149-f0952efe572a</id>
      <classConcept>7c08bd55-4d42-49cd-92f8-6388d6c4183f</classConcept>
      <determinerConcept>f29f08de-78a7-4a5e-aeaf-7b545ba19a09</determinerConcept>
      <statusConcept>c8064cbd-fa06-4530-b430-1a52f1530c27</statusConcept>
	    <industryConcept>fdeb2e4e-9e02-4ce3-ab69-cece5ffdee20</industryConcept>
      <name>
        <use>1ec9583a-b019-4baa-b856-b99caf368656</use>
        <component>
          <value>Elbonia National Health Insurnace Corporation</value>
        </component>
      </name>
    </Organization>
  </update>  
  <update insertIfNotExists="true">
    <SecurityPolicy xmlns="http://santedb.org/model">
      <id>fd8c0e00-82fb-11eb-8dcd-0242ac130004</id>
      <name>Elbonia Parlimentarian Health Record VIP Access Policy</name>
      <oid>2.25.40394829382872728372832</oid>
      <isPublic>true</isPublic>
      <canOverride>false</canOverride>
    </SecurityPolicy>
  </update>  
</dataset>
```

The file would be copied into the /santedb/data directory of the santedb-mpi or santedb-icdr container with the following Dockerfile.

```markup
FROM santedb-icdr:latest
COPY custom.dataset /santedb/data/custom.dataset
```

### Packaging Custom Business Rules

You can package [business rules](../../../extending-santedb/applets/business-rules.md), [business intelligence](../../../extending-santedb/applets/business-intelligence-bi-assets/), and other [asset files](../../../extending-santedb/applets/assets/) into your docker container by simply composing them into a PAK file and including them in the /santedb/applets/ directory.

```markup
FROM santedb-icdr:latest
COPY custom.pak /santedb/applets/custom.pak
```

Upon load, the SanteDB iCDR server will load your package files and will load any business rules files required.


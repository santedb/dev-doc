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

### Advanced Configurations

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




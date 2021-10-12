# Configuration Tool

The SanteDB configuration tool is a graphical tool which is used to control the [SanteDB Configuration](../../../operations/host-administration/host-configuration-file/) file.

## Initial Configuration

Whenever you install SanteDB in a new environment you will be prompted to run the Configuration Tool. On initial configuration the configuration tool will show its initial configuration screen.

![Initial Configuration](<../../../../.gitbook/assets/image (418).png>)

The options are:

* **Easy Configuration** -> Sets a series of defaults from the selected **Template**
* **Advanced Configuration **-> Creates an empty configuration file which administrators can use individual configuration panels to control the overall configuration.

In most cases the Easy Configuration should be used.

### Database Configuration

To setup Easy Configuration select the database software you'll be using and enter the connection details for the configuration.

#### PostgreSQL Configuration

When PostgreSQL is selected as the database software, you should enter the connection details to the PostgreSQL server and database you'd like to configure.

| Option      | Description                                                                                      | Example   |
| ----------- | ------------------------------------------------------------------------------------------------ | --------- |
| host        | The location of the PostgreSQL server on your network.                                           | localhost |
| port        | The port number (if using a different port than 5432)                                            | 5432      |
| user id     | The user identifier which SanteDB should use to connect to the database server.                  |           |
| password    | The password for the user to be used to connect to the server.                                   |           |
| database    | The name of the database to connect to (or a new database)                                       |           |
| pooling     | True if the SanteDB should use connection pooling (true recommended for production environments) |           |
| minpoolsize | The minimum number of pooled connections to keep open to the database.                           | 5         |
| maxpoolsize | The maximum number of pooled connections to allow to the database (before a wait is induced)     | 20        |

#### Firebird

When Firebird is selected as the database software, SanteDB will assume you're using an embedded IBSQL (Firebird) database.

| Option          | Description                                                                | Example |
| --------------- | -------------------------------------------------------------------------- | ------- |
| user id         | The user identifier to connect to the database provider (should be SYSDBA) | SYSDBA  |
| password        | If password protecting the database, the password of SYSDBA                |         |
| initial catalog | The name of the FDB file to connect to or a new database.                  |         |

#### Creating a new Database

You can create a new database from the configuration tool on the database software of your choice by selecting New Database as the database option. You will be prompted to enter the details of the database you're creating:

![](<../../../../.gitbook/assets/image (417).png>)

You will need to provide the superuser account of a user which has `CREATE DATABASE` permission on the selected provider. Upon pressing OK the database will be created and initialized, and you will be returned to the initial configuration screen.

### Instance Name

If you're running multiple copies of SanteDB on the same server environment, the named instance is the differentiation between these instances. The configuration tool will register the appropriate instance name service on your Windows operating system to start/stop the instance.

### Template

SanteDB iCDR servers have hundreds of configuration options. The `Template` option allows you to quickly select a configuration template which has pre-configured values as a starter for your configuration. The templates which are commonly used are:

* SanteDB MDM -> Configuration with Master Data Management enabled
* SanteMPI Server -> Configuration with the SanteMPI interfaces pre-configured
* SanteGuard Server -> Configuration with the SanteGuard interfaces pre-configured.

If you do not select a template, you will need to configure each plugin in the S

# Database Connections

On the initial configuration screen, as well as any configuration page which requires a connection to be set, the tool exposes a panel for connection string editing.

Connection strings are named settings which provide SanteDB with the necessary information to contact a particular database server using a specified provider.&#x20;

## Editing Connection Strings

When editing a connection string in an existing configuration file, you will be presented with a list of connection strings which have already been configured:

![](<../../../../.gitbook/assets/image (86).png>)

In the example above, a user could select a an existing Read/Write connection string which has already been configured or they can create a NEW connection string to, for example, bind the read/write connection string to a read/write primary node.

![](<../../../../.gitbook/assets/image (439).png>)

## Connection Types

### PostgreSQL Configuration

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

### Firebird

When Firebird is selected as the database software, SanteDB will assume you're using an embedded IBSQL (Firebird) database.

<table><thead><tr><th>Option</th><th width="222.33333333333331">Description</th><th>Example</th></tr></thead><tbody><tr><td>user id</td><td>The user identifier to connect to the database provider (should be SYSDBA)</td><td>SYSDBA</td></tr><tr><td>password</td><td>If password protecting the database, the password of SYSDBA</td><td></td></tr><tr><td>initial catalog</td><td>The name of the FDB file to connect to or a new database.</td><td></td></tr></tbody></table>

### SQLite / SQLCipher

SanteDB iCDR version 3.0 and higher supports the configuration of the SQLite and SQLCipher persistence layer. This is ideal for test environments and lightweight deployments.

<table><thead><tr><th>Option</th><th width="222.33333333333331">Description</th><th>Example</th></tr></thead><tbody><tr><td>data source</td><td>The name of the SQLite database file which should be used for connection</td><td>test.sqlite</td></tr><tr><td>password</td><td>If using SQLCipher the password indicates the passkey for the encrypted database.</td><td></td></tr><tr><td>foreign keys</td><td>True when the SQLite engine should enforce foreign keys.</td><td></td></tr></tbody></table>

## Creating a new Database

You can create a new database from the configuration tool on the database software of your choice by selecting New Database as the database option. You will be prompted to enter the details of the database you're creating:

![](<../../../../.gitbook/assets/image (281).png>)

You will need to provide the superuser account of a user which has `CREATE DATABASE` permission on the selected provider. Upon pressing OK the database will be created and initialized, and you will be returned to the initial configuration screen.

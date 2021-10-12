# SanteDB iCDR

The SanteDB iCDR server runs via the SanteDB.exe file located in the following default installation directories:

* **Microsoft Windows Operating Systems: **C:\Program Files\SanteSuite\SanteDB\Server\SanteDB.exe
* **Linux Operating Systems: **/opt/sante-suite/santedb/server/SanteDB.exe

This process can be used to operate one or more IMS services. 

## Getting Started

### Configuration of Host

When you install the SanteDB iCDR server, the application (by default) has no configuration file. The default configuration file is `santedb.config.xml` , this file can be created by running `ConfigTool.exe` ([as illustrated here](broken-reference)) or by copying one of the sample files. The sample configuration files are:

* santedb.config.psql.xml - A basic configuration file which is setup to run with PostgreSQL server.
* santedb.config.fbsql.xml - A basic configuration file which is designed to operate with Firebird databases (Windows only)
* Generated - You can generate an empty configuration file by running `SanteDB.exe --genconfig` and then editing the resulting default.config.xml file that is created.

For more information, see the [SanteDB Configuration](host-configuration-file/) documentation.

### Command Options

The following options can be used on the SanteDB.exe command

| Option          | Use                                                     | Example             |
| --------------- | ------------------------------------------------------- | ------------------- |
| --console       | Run as an application rather than a service.            | --console           |
| --test-startup  | Tests the configuration file (for startup) then stops . | --test-startup      |
| --name=INSTANCE | Named instance to configure as a windows service        | --name=IMS1         |
| --config=file   | Load an alternate configuration file                    | --config=myconf.xml |
| --genconfig     | Generate an empty configuration file.                   |                     |

### Running in Linux / MacOS

To run the SanteDB.exe process in a terminal you can the following command:

`mono /opt/sante-suite/santedb/server/SanteDB.exe --console`

Additionally the service can be installed into your operating system by copying the service definition from /opt/sante-suite/santedb/server/santedb.service to your distribution's appropriate directory.

Then you can control the service by running:

`systemctl start santedb`

### Folder Structure

The SanteDB iCDR server uses a folder structure as illustrated below.

![](<../../../.gitbook/assets/image (187).png>)

The folders are:

* applets - Applet PAK files which control the behavior, business rules, BI definitions, and common user interface elements. These files are documented more in the [Applets](../../extending-santedb/applets/) wiki page.
* data - Dataset files which are installed by the SanteDB host service on start. These files contain common terminology, identity domains, places, etc. See the [Dataset Files](../../extending-santedb/applets/distributing-data.md) wiki page.
* plugins - This folder is used by FirebirdSQL to load custom SQL plugins.
* queue - This folder is the default location of the file-system based persistent queue service. This directory stores outbound messages and has a dead-letter queue for retry. 
  * Note: Future persistent queue plugins may use databases or queue technologies in lieu of this directory.
* match - This folder contains one or more match definition files and is the default directory for the file system match configuration provider.
  * Note: Future match configuration providers will use databases or other technologies for storing/reading match configurations.
* sql  - This folder contains SQL files that you will need to deploy the SanteDB databases including:
  * fbsql/ - Core SQL in Firebird SQL syntax to create a new database
  * psql/ - Core SQL in PL/PGSQL syntax to create a new database
  * updates/ - Patches to the database which should be applied in-order

### Log Files

Log files are located at %installdir%/santedb_YYYYMMDD.log and have a format as described below:

```
Source@ThreadID <Level> [TIMESTAMP]: Log Message
```

For example, this log entry indicates an ERROR on 2021-01-05 from the FHIR plugin on thread 7:

```
SanteDB.Messaging.FHIR@RSRVR-ThreadPoolThread-7 <Error> [2021-01-05T00:45:15.9914111-05:00]: Error on WCF FHIR Pipeline: SanteDB.Core.Exceptions.PolicyViolationException: Policy '1.3.6.1.4.1.33349.3.1.5.9.2.2.0' was violated by 'Administrator' with outcome 'Deny'
```

Using the ThreadID is helpful when diagnosing issues in a production environment as it allows for the tracking of a client's execution pathway through the solution.

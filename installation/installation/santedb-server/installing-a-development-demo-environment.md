# Installation on Microsoft Windows

When installing SanteDB iCDR server on a Microsoft Windows Server environment you should use the installation package for the latest version of the SanteDB iCDR server. Each solution within SanteDB iCDR Server has its own distribution which can be downloaded for their own source repository.&#x20;

* [SanteDB iCDR Releases](https://github.com/santedb/santedb-server/releases)
* [SanteMPI Releases](https://github.com/santedb/santempi/releases)

The installation process for SanteDB on Microsoft Windows is a three step process:

1. [Install the software](installing-a-development-demo-environment.md#installation)
   * Copy software program files and pre-requisites&#x20;
   * Initiate the configuration process
2. [Configuration of the software](installing-a-development-demo-environment.md#configuration)
   * Customizing the behavior of the installed plugins
   * Entering implementation specific details about the deployment
3. Running/Initializing the Server

## System Requirements

When running SanteDB iCDR server on Microsoft Windows you will require, at minimum:

* Microsoft Windows Server 2012 Standard or Microsoft Windows 10
* 2 Core CPU (4 to 8 Cores recommended)
* 2 GB RAM (8 or 16 GB of RAM recommended)
* 300 MB of disk space (1 GB recommended)

Users should be familiar with basic Microsoft Windows concepts such as:

* Basic familiarity with the Windows Command Line
* Basic familiarity with Microsoft Management Console (MMC)
* Basic familiarity with Windows Networking

## Installation

The installation programs on Windows will:

* Install the Visual C++ 2010 redistributable (for C++ libraries)
* Install Microsoft .NET Framework 4.8 (if not already installed)
* Copies the required files for the selected options to the Installation&#x20;
* Opens Firewall port 8080 and 2100 (for HL7v2) on the Windows Firewall
* Create an un-installer which will clean the directory on uninstall

The installation process is a standard Windows installer experience, administrators can elect to install particular plugins that meet their needs.&#x20;

![](<../../../.gitbook/assets/image (420) (1) (1) (1) (1) (1) (1).png>)

The plugins available at the time of writing are enumerated below.

{% hint style="info" %}
You should reduce the attack surface area of SanteDB iCDR by only installing the plugins which your deployment and use case requires. For example, installing the MDM plugin on an IMS may not make sense in that context - and installation of the MDM plugin would expose new API endpoints over REST which may increase the attack surface area of the iCDR server.
{% endhint %}

#### SanteDB Core

The SanteDB Core option installs the core Windows Service executable (`santedb.exe`), as well as baseline files such as the API libraries, etc.

#### JINT Business Rules Engine

The JINT business rules engine allows applets to customize the iCDR and dCDR application behavior by writing [JavaScript Business Rules](../../../developers/extending-santesuite/extending-santedb/applets/business-rules.md#introduction).

#### XML Clinical Support Decision Engine

If your installation of the iCDR will be [using clinical decision support ](../../../developers/extending-santesuite/extending-santedb/applets/cdss-protocols.md#introduction)(CDSS) via the built-in XML protocol format, you should enable CDSS support.

#### Messaging Interfaces

The messaging interfaces option installs the core REST APIs for the iCDR server. These messaging interfaces allow administrators to customize their deployment for scale-out by assigning servers to dedicated roles. For example, in a scaled-out solution an administrator may only install the [Administrative Management Interface](../../../developers/extending-santesuite/extending-santedb/service-apis/administration-management-interface-ami/) to the server which controls the cluster, whereas other servers may only install the [Health Data Services Interfaces](../../../developers/service-apis/health-data-service-interface-hdsi.md#controlling-response-format) for clinical data access.

#### Business Intelligence Services

When installed, the SanteDB core business intelligence services for rendering and executing reports from applets will be enabled. The BIS should be installed on servers where you'd like the clients to be able to access shared report definitions.&#x20;

If you're using a third party reporting tool like Jasper Reports, Crystal Reports, SQL Server Report Services, etc. you do not need to enable this.

#### Integration Interfaces

Installation of the integration interfaces will allow SanteDB iCDR to interact with third party services using one of the standards based APIs such as:

* [HL7 Fast Health Interoperability Resources](../../../operations-1/standard-operating-procedures/hl7-fhir/)
* [HL7 Version 2](../../../developers/service-apis/hl7v2.md)&#x20;
* [GS1 Business Messaging Standard (BMS)](../../../developers/santedb-software-publishers/gs1-bms-xml/#gs1-stock-messaging-workflows)
* JIRA Integration (which allow submission of Diagnostic reports from dCDR instances directly into JIRA)
* ATNA & DICOM Messaging (which allows for dispatch of audits via NEMA DICOM over Syslog)

#### Two-Factor Authentication

Installation of a TFA provider allows the iCDR to leverage multi-factor authentication workflows using either E-Mail based TFA codes or SMS based TFA codes (via Twilio)

#### Master Data Management

Installation of the MDM plugin copies the necessary plugins to enable the Master Data Management Resource Manager.

#### Data Persistence

The data persistence plugins enable the one or more of the persistence services in SanteDB on the server. The persistence layer plugins supported are:

* PostgreSQL Server Plugin
* Firebird Plugin

#### Caching Services

You should install , at a minimum the **Memory Caching** service plugin to improve the performance of your installation. If you're running SanteDB in a shared environment with multiple servers in a cluster environment, installation of REDIS is recommended.

#### Elbonia Quickstart

Installing the Elbonia Quickstart pack will seed your SanteDB instance with sample data from the fake jurisdiction (from Dilbert) of Elbonia.

## Configuration

Configuration of the SanteDB service is covered in a series of discrete wiki articles which cover each configuration option in the platform and their impact on the system.

Configuration of the SanteDB server should be done prior to the first start of the software. The option to start the configuration tool for SanteDB is provided at the end of the SanteDB installation process.

See: [configuration-tool](../../../operations/server-administration/configuration-tool/ "mention")

When first configuring SanteDB iCDR server on a Windows environment you will need to select the database persistence technology the server will be using, the options are:

* PostgreSQL 9+ :  If you're running SanteDB with full functionality, select this option.
* Firebird : If you're running SanteDB for a quick demonstration or test, select this option.

#### PostgreSQL Configuration

Selecting the PostgreSQL provider will expose the connection parameters for PostgreSQL. See [#postgresql-configuration](../../../operations/server-administration/configuration-tool/persistence-settings/database-connections.md#postgresql-configuration "mention") for more information on these settings.

![](<../../../.gitbook/assets/image (428) (1) (1) (1) (1) (1) (1).png>)

#### Firebird Configuration

Selecting the Firebird provider will expose the connection parameter for Firebird 3.x provider, SanteDB iCDR will assume you're using the embedded version of Firebird. This database connector has three parameters. See [#firebird](../../../operations/server-administration/configuration-tool/persistence-settings/database-connections.md#firebird "mention") connection details in the configuration tool documentation.

![](<../../../.gitbook/assets/image (426) (1) (1) (1) (1).png>)

#### Multiple Instances of SanteDB on the Same Server

If you're running multiple instances of SanteDB on the same server, you will need to install the software in different file locations. When configuring the iCDR on the Windows host you can then set an instance name to isolate the Windows Services and event logs.

![](<../../../.gitbook/assets/image (418) (1) (1).png>)

#### Configuration Template

SanteDB iCDR server packages may be shipped with one ore more [santedb-solutions.md](../../../santedb/santedb-solutions.md "mention") included, you should select an appropriate template for the software solution that this instance of the iCDR will fulfill.

![](<../../../.gitbook/assets/image (437) (1) (1) (1) (1) (1) (1) (1) (1).png>)

#### Initial Configuration Tasks

Once you've completed the installation options for the SanteDB server and press `Continue` you will be prompted to confirm the initial configuration tasks.

![](<../../../.gitbook/assets/image (448) (1) (1) (1) (1) (1) (1).png>)

#### Finish Configuration&#x20;

You can use the configuration tooling to customize your installation of the SanteDB server. These settings are documented in [configuration-tool](../../../operations/server-administration/configuration-tool/ "mention")

![](<../../../.gitbook/assets/image (444) (1) (1) (1) (1) (1) (1).png>)

Recommended configuration panels and settings to change include:

* Changing the Performance/Caching to REDIS caching and setting up REDIS
* Turning down the Diagnostics/Logging setting to Warning or Error

## Initial Run / Initialization

After you have applied the configuration from the Configuration Tool, the SanteDB service will automatically restart.&#x20;

{% hint style="info" %}
If you're using the Firebird based database for SanteDB iCDR you will need to exit the configuration tool after applying your configuration (since the configuration tool locks the database file). After this you may restart the service manually (see [#service-management](installing-a-development-demo-environment.md#service-management "mention"))
{% endhint %}

### Validating Installation

Once started you can validate connectivity to the SanteDB iCDR server by accessing the Start menu and running `SanteDB Server Console (localhost)` . You should be prompted with a login prompt.

{% hint style="info" %}
If the window closes immediately, the server may not be completed startup. Check the `C:\Program Files\SanteSuite\SanteDB\Server\Data` directory. You should see the files have been initialized if the directory contains no `.dataset` files , and instead contains `.completed` files.
{% endhint %}

Once the login prompt is available you can login with `Administrator` and password `Mohawk123`.

```
SanteDB Administration & Security Console v2.1.131.0 (Queenston)
Copyright (C) 2015 - 2020, SanteSuite Community Partners (see NOTICES)
Access denied, authentication required.
Username:administrator
Password:************
* http://localhost:8080/ami -> v.2.1.116.0 (Queenston)
Ready...
>
```

### Service Management

SanteDB runs as a Windows service (equivalent of a daemon). These can be accessed using the `services.msc` plugin an finding the `SanteDB Host Process` service. Additionally the service can be restarted from an elevated command prompt using:

```
C:\Users\user> NET STOP santedb
C:\Users\user> NET START santed
```

{% hint style="info" %}
If you're running multiple instances of SanteDB on the same server as named instances, each instance of the host process will be `SanteDB Host Process -` name
{% endhint %}


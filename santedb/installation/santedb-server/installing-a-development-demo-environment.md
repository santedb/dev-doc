# Standalone Server

When installing SanteDB iCDR server on a Microsoft Windows Server environment you should use the installation package for the latest version of the SanteDB iCDR server. Each solution within SanteDB iCDR Server has its own distribution which can be downloaded for their own source repository.&#x20;

* [SanteDB iCDR Releases](https://github.com/santedb/santedb-server/releases)
* [SanteMPI Releases](https://github.com/santedb/santempi/releases)

The installation process for SanteDB on Microsoft Windows is a three step process:

1. Install the software:
   * Copies software program files and pre-requisites&#x20;
   * Creates an un-installer
   * Initiates the next step of the process
2. Configuration of the software:
   * Customizing the behavior of the installed plugins
   * Entering implementation specific details about the deployment
3. Running/Initializing the Server

## Installation

Each of these installers:

* Install the Visual C++ 2010 redistributable (for C++ libraries)
* Install Microsoft .NET Framework 4.8 (if not already installed)
* Copies the required files for the selected options to the Installation&#x20;
* Opens Firewall port 8080 and 2100 (for HL7v2) on the Windows Firewall
* Creates an un-installer which will clean the directory on uninstall

### Windows Installer

The installation process is a standard Windows installer experience, administrators can elect to install particular plugins that meet their needs.&#x20;

![](<../../../.gitbook/assets/image (420) (1) (1) (1) (1).png>)

The plugins available at the time of writing are enumerated below.

{% hint style="info" %}
You should reduce the attack surface area of SanteDB iCDR by only installing the plugins which your deployment and use case requires. For example, installing the MDM plugin on an IMS may not make sense in that context - and installation of the MDM plugin would expose new API endpoints over REST which may increase the attack surface area of the iCDR server.
{% endhint %}

#### SanteDB Core

The SanteDB Core option installs the core Windows Service executable (`santedb.exe`), as well as baseline files such as the API libraries, etc.

#### JINT Business Rules Engine

The JINT business rules engine allows applets to customize the iCDR and dCDR application behavior by writing [JavaScript Business Rules](../../extending-santedb/applets/business-rules.md#introduction).

#### XML Clinical Support Decision Engine

If your installation of the iCDR will be [using clinical decision support ](../../extending-santedb/applets/cdss-protocols.md#introduction)(CDSS) via the built-in XML protocol format, you should enable CDSS support.

#### Messaging Interfaces

The messaging interfaces option installs the core REST APIs for the iCDR server. These messaging interfaces allow administrators to customize their deployment for scale-out by assigning servers to dedicated roles. For example, in a scaled-out solution an administrator may only install the [Administrative Management Interface](../../extending-santedb/service-apis/administration-management-interface-ami/) to the server which controls the cluster, whereas other servers may only install the [Health Data Services Interfaces](../../extending-santedb/service-apis/health-data-service-interface-hdsi/#controlling-response-format) for clinical data access.

#### Business Intelligence Services

When installed, the SanteDB core business intelligence services for rendering and executing reports from applets will be enabled. The BIS should be installed on servers where you'd like the clients to be able to access shared report definitions.&#x20;

If you're using a third party reporting tool like Jasper Reports, Crystal Reports, SQL Server Report Services, etc. you do not need to enable this.

#### Integration Interfaces

Installation of the integration interfaces will allow SanteDB iCDR to interact with third party services using one of the standards based APIs such as:

* [HL7 Fast Health Interoperability Resources](../../extending-santedb/service-apis/hl7-fhir/)
* [HL7 Version 2](../../extending-santedb/service-apis/hl7v2/)&#x20;
* [GS1 Business Messaging Standard (BMS)](../../extending-santedb/service-apis/gs1-bms-xml.md#gs1-stock-messaging-workflows)
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

### Linux Servers

When installing using the tarball on Linux the process is manual - the instructions here are for Ubuntu based Linux Servers at `/opt/santedb`

## Configuration

Configuration of the SanteDB service is covered in a series of discrete wiki articles which cover each configuration option in the platform and their impact on the system.

See: [Configuration Tool Documentation](../../operations/host-administration/configuration-tool/)

## Service Management

SanteDB runs as a Windows service (equivalent of a daemon). These can be accessed using the `services.msc` plugin an finding the `SanteDB Host Process` service.

{% hint style="info" %}
If you're running multiple instances of SanteDB on the same server as named instances, each instance of the host process will be `SanteDB Host Process - `name
{% endhint %}


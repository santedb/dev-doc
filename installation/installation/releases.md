# Releases

SanteDB software can be downloaded via the GitHub pages for each of the projects.

## Downloads

| Download Link                                                                      | Contents                                                                                                        | Installation Instructions                                                                                                                            |
| ---------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| [SanteDB iCDR](https://github.com/santedb/santedb-server/releases)                 | <ul><li>SanteDB iCDR Server</li><li>SanteDB Administration Console</li></ul>                                    | [santedb-server](../installation-1/deployment/software-deployment/santedb-server/ "mention")                                                         |
| [SanteMPI iCDR](https://github.com/santedb/santempi/releases)                      | <ul><li>SanteMPI Server</li></ul>                                                                               | [santedb-server](../installation-1/deployment/software-deployment/santedb-server/ "mention")                                                         |
| [SanteDB dCDR Web Access Gateway](https://github.com/santedb/santedb-www/releases) | <ul><li>Web Access Gateway Service</li></ul>                                                                    | [installing-web-access-gateway.md](../installation-1/deployment/software-deployment/disconnected-gateway/installing-web-access-gateway.md "mention") |
| [SanteDB dCDR SDK](https://github.com/santedb/santedb-sdk/releases)                | <ul><li>Applet Debugger</li><li>Business Rules Debugger</li><li>Data Importer</li><li>Package Manager</li></ul> | [installing-the-dcdr-sdk.md](../installation-1/deployment/software-deployment/disconnected-gateway/installing-the-dcdr-sdk.md "mention")             |

{% hint style="info" %}
You can download the latest versions (even if release notes aren't prepared for them on GitHub) from the [SanteDB Experimental Releases](http://santesuite.org/assets/uploads/santedb/community/releases/) repository.
{% endhint %}

## SanteDB iCDR Server&#x20;

### Installers

The following iCDR server releases can be found via the [santedb-server project ](https://github.com/santedb/santedb-server/releases)on GitHub:

* Microsoft Windows Installation Package
* Linux Distribution (manual install via tarball)
* MacOS (manual install via zip)

### Virtual Appliances

Additionally, you can download a virtual appliance via an Open Virtual Appliance file:

* [Headless Virtual Appliance](http://santesuite.org/assets/uploads/santedb/community/ova/santempi-latest-headless.ova) (useful for running SanteDB in a production environment)
* [Developer Virtual Appliance ](http://santesuite.org/assets/uploads/santedb/community/ova/santempi-latest-developer.ova)(useful for developers working with SanteDB)

### Docker Containers

You can also run SanteDB iCDR products in a Docker or Kubernetes environment. For more details see the [Docker Containers ](../installation-1/deployment/software-deployment/santedb-server/installation-using-appliances/docker-containers/)documentation.

## SanteDB dCDR

### Android Application

Typically a SanteDB dCDR instance is customized and branded for a particular context. You can download the vanilla (whitelabel) dCDR Android Applications via the [santedb-dc-android GitHub ](https://github.com/santedb/santedb-dc-android/releases)project.

{% hint style="info" %}
You can use the generic SanteDB dCDR Android application to connect to any SanteDB iCDR server - the generic dCDR will download the latest application packages from the iCDR after joining.
{% endhint %}

### Windows Application

The self-contained Windows Application is useful for disconnected environments where larger datasets are required offline and higher burden of data entry is necessary. The Windows Application can be installed via the installers available on the [santedb-dc-win32 GitHub](https://github.com/santedb/santedb-dc-win32/releases) project.

### Disconnected Gateway Service

The disconnected gateway service provides a common dCDR instance running on a local area network and allows multiple web-browsers, Android apps, and third party systems (via HL7 or FHIR) to connect to the disconnected environment.

The dCDR can be installed and is tested on:

* Microsoft Windows via an installer
* Linux or MacOS via a tarball/zip distribution (requires Mono framework)
* Raspbian or MacOS M1 ARM processors (requires Mono for ARM)

The dCDR Gateway can be downloaded from the [santedb-dcg GitHub](https://github.com/santedb/santedb-dcg/releases) project.

### dCDR Web Access Gateway

The dCDR WWW service allows operators of SanteDB infrastructure to host dCDR applications (which are typically designed for offline use) to operate in an online-only fashion and allows for access to the user interfaces for broad internet hosting environments.

The dCDR web host is typically used to host administrative panels, reporting portals, etc. The service can be installed on:

* Microsoft Windows (via installer)
* Linux or MacOS (via tarball - requires Mono Framework)
* Docker Containers

The installers can be accessed via the [santedb-www GitHub](https://github.com/santedb/santedb-www/releases) project. The docker instance can be spun up using the `santedb-www:latest` docker image.

## Software Development Kit

The SanteDB SDK is used by developers to simulate the offline dCDR in a debug-friendly environment. The SDK is documented on the [installing-the-dcdr-sdk.md](../installation-1/deployment/software-deployment/disconnected-gateway/installing-the-dcdr-sdk.md "mention") wiki page.&#x20;

The SDK runs on:

* Microsoft Windows (via installer)
* Linux or MacOS (via tarball - requires Mono Framework)

It can be downloaded from the [santedb-sdk GitHub](https://github.com/santedb/santedb-sdk/releases) project page.

# Installing Web Access Gateway

The SanteDB web access gateway is a specialized dCDR instance which permits accessing SanteDB instances over the internet. The dCDR Web Access Gateway allows users with an internet connection and a web-browser to access SanteDB Applets.

Use cases for installing the Web Access Gateway include:

* The centralized [Administration Panel](../../../operations/cdr-administration/)&#x20;
* A centralized jurisdictional portal to an IMS interface
* A centralized Audit Repository User Interface

The web access gateway is deployed in two steps:

1. Installing the Software Services&#x20;
2. Joining the central iCDR security domain

## System Requirements

The minimum system requirements for installing the Web Access Gateway on a physical or virtual operating environment are as follows:

* Microsoft Windows Server 2012 Standard, or
* Ubuntu Linux 18.04 or equivalent distribution
* 2x CPU Cores (4x recommended)
* 2 GB RAM  (4 GB recommended)
* 100 MB of HDD space (1 GB recommended)

## Installing Software Services

You can obtain the SanteDB Web Access Gateway software from the [SanteDB WWW GitHub Project](https://github.com/santedb/santedb-www/releases).

{% hint style="warning" %}
Installation of the Web Access Gateway should be performed on machines, containers, or VMs on the same physical network as the central iCDR server. Additionally, it is recommended that the iCDR and Web Access Gateway communicate on the protected, internal network over HTTP rather than HTTPS (to reduce the overhead of establishing SSL communications on an already physically secured network).
{% endhint %}

### Installation on Microsoft Windows

Installation of the Web Access Gateway on Microsoft Windows Operating Systems is a standard Windows Installer experience. The application installer will copy the&#x20;

![](<../../../.gitbook/assets/image (429) (1) (1) (1).png>)

After installation is complete you will be asked to [Configure the Web Access Gateway](installing-web-access-gateway.md#undefined).

#### Upgrading Web Access Gateway Software on Windows

When updating the SanteDB Web Access Gateway, you should use the installer provided for the new version. The installers for the Web Access Gateway are able to restart services and perform partial upgrades of the program files installed.&#x20;

You may receive a notice to restart existing running services. It is safe to select `Automatically Close Applications`.

![](<../../../.gitbook/assets/image (431) (1) (1).png>)

### Installation on Linux Operating Systems

{% hint style="info" %}
We're currently writing this section. Check back soon!
{% endhint %}

### Using Docker Containers

You can use the `santedb-www:latest` Docker container to leverage the SanteDB web access gateway by adding a `www` container reference to your `docker-compose.yml` file and redirecting port 9200 to an appropriate outside port.

```yaml
  www:
    image: santesuite/santedb-www:latest
    container_name: santedb-www
    ports:
      - "9200:9200"
    depends_on:
      - santedb
    restart: always
```

Once configured you can access the portal by navigating to : http://localhost:9200

{% hint style="warning" %}
Never expose the SanteDB WWW host container to the internet. If you are running the santedb-www container and wish to expose it to external clients, it is recommended you use SSL termination with either IIS or NGINX. See [securing-the-apis.md](../securing-the-apis.md "mention")
{% endhint %}

## Configure the Web Access Gateway

After installation is complete you can navigate to `http://127.0.0.1:9200` in a support web browser (the Web Access Gateway is tested with Chrome, Firefox, and Microsoft Edge).&#x20;

The configuration screen for the web access gateway is identical to the configuration screen for the Disconnected Gateway, except the online mode is the only mode supported.

### Join the Security Domain

![](<../../../.gitbook/assets/image (442) (1) (1) (1).png>)

* **Local Device ID**: The device identifier which this web access gateway will use to enrol itself in the iCDR security domain (example: `admin-portal` or `admin-portal-cluster-1`)
* **Domain Address**: The IP address or host name of the iCDR server instance. If you're running the iCDR in a distributed deployment, this should be the address to a machine or group running the [administrative-management-interface.md](../../../operations/server-administration/configuration-tool/messaging-settings/administrative-management-interface.md "mention")  .
* **Client Secret Mode**: If you have configured the SanteDB OAUTH services (or are using a third party IdP) to use client secrets in the `Authorization` header , set this `HTTP BASIC` otherwise leave this as the default.
* **Application Secret Override**: If your deployment has changed the default application secret for the application `org.santedb.disconnected_client` then you should set it here.
* **iCDR Administrative Port**: The port where the SanteDB iCDR is listening for traffic
* **Use TLS/SSL**: When communicating with a remote server, you should select this option.

Pressing the **JOIN** button will require you to login as the system administrator for the SanteDB server.

![](<../../../.gitbook/assets/image (436) (1) (1) (1).png>)

You should use the administrative user account and password to authenticate yourself with the domain.

### Set Web Access Gateway Role

A single SanteDB iCDR server can host multiple SanteDB solutions and user interfaces. For example, an iCDR for SanteMPI may contain the SanteMPI administrative interface, an end-user registration interface, and a variety of other applications.&#x20;

When configuring the SanteDB Web Access Gateway (like all dCDR instances) you must select the application role that the SanteDB dCDR will be taking on.

![](<../../../.gitbook/assets/image (445) (1) (1) (1) (1) (1) (1) (1).png>)

Additionally, it is recommended that you select SanteDB to automatically update applets on the Web Access Gateway. &#x20;

![](<../../../.gitbook/assets/image (441) (1) (1) (1) (1) (1).png>)

{% hint style="info" %}
The SanteDB dCDR software packages like the Windows Application, Android Application and dCDR Gateway may opt to not auto-update applets depending on bandwidth restrictions.
{% endhint %}

## Set Synchronization Mode to Online

Since the SanteDB Web Access Gateway is intended to be used in an environment where it can always communicate with the iCDR server directly, and because it lacks the storage capacity to operate offline, the synchronization mode of the Web Access Gateway should be set to Online Only.

![](<../../../.gitbook/assets/image (446) (1) (1) (1) (1) (1).png>)

### Set Log Verbosity

By default, SanteDB Web Access Gateway release builds will only log events which are errors or warnings. If you desire more verbose logging you can alter the setting for logging in this panel.

![](<../../../.gitbook/assets/image (421) (1) (1) (1) (1).png>)

### Application Services

It is recommended you leave the default application services selected for the Web Access Gateway. These settings are primarily intended for disconnected client gateways which require fine tuning of HL7, FHIR, ATNA and other services for local clinics.

![](<../../../.gitbook/assets/image (444) (1) (1) (1) (1) (1) (1).png>)

### Set Networking Parameters

By default, the SanteDB dCDR instances will optimize traffic with the central iCDR using one of BZIP, GZIP, deflate, or LZMA compression (depending on the network infrastructure). The network optimization panel allows you to tell SanteDB about the networking environment in which this dCDR instance is running.

If you're running the iCDR server on the same machine as the Web Access Gateway or are using a 10gbE connection between the two, you can set this to Local Network, since this will disable all compression (saving compute resources). If you are running the Web Access Gateway and iCDR in an environment which has a slower connection between the iCDR and dCDR it may be beneficial to select another option.

![](<../../../.gitbook/assets/image (443) (1) (1) (1) (1) (1) (1).png>)

| Optimization Setting | Compression Used |
| -------------------- | ---------------- |
| Local Network        |  None            |
| Very Fast            | deflate          |
| Fast                 | gzip             |
| Moderate             | bzip2/9          |
| Slow                 | LZMA/max         |

You may also optionally proxy traffic flowing between the Web Access Gateway and the iCDR instance by enabling the **Use a proxy to access the server.** This is useful if you're diagnosing performance bottlenecks between the systems, or the data center requires proxying.

### Other Settings

The other settings panel allows you to configure custom behaviors for the Web Access Gateway. These settings are documented on the [app-settings.md](app-settings.md "mention")wiki page.

![](<../../../.gitbook/assets/image (430) (1) (1) (1) (1) (1).png>)

{% hint style="info" %}
You can change the application settings for the Web Access Gateway after initial configuration via the file `%systemroot%\Windows\SYSWOW64\config\systemprofile\AppData\Roaming\SanteDB\wwww-default` on Windows or via `~/.config/santedb/santedb-www` on Linux and Docker.
{% endhint %}

### Restart Web Access Gateway

After the setup is complete you will be notified that your configuration has been saved and will wait for an application restart. This process typically takes between 10 and 20 seconds. The page should automatically refresh.&#x20;

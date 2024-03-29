# System Settings

The system settings group of features is used to control core system functions related to SanteDB iCDR. In general system settings should never need to be altered from the template unless special requirements for hosing queues, applets, and other services on shared drives is a requirement.

## File System Manager Queue

Some SanteDB services which need to send messages will use a persistence queue to store messages in case of delivery failure. The File System Manager queue is a simple queue which uses the local file system as a persistent queue (there are future work items for MSMQ and other technologies).

![](<../../../.gitbook/assets/image (497).png>)

The only setting for the file system queue is the local directory / path where the persistent queue messages should be stored.

## Microsoft Messaging Queue

The Microsoft Messaging Queue configuration panel allows SanteDB iCDR to send queue messages to an MSMQ server (either local or remote). This has a performance benefit in that MSMQ is well suited for higher traffic scenarios than the file system manager.

![](<../../../.gitbook/assets/image (434) (1) (1) (1).png>)

The configuration setting for `MSMQ Path` should be in one of the following formats:

| Local Queue (Private) | `.\$Private`         | Stores queue messages in a private queue space. A private queue is owned by the `SanteDB Host Process` user and other users are not permitted access to the queue. If administration of the queue is required, run the SanteDB Host Process as a service account. |
| --------------------- | -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Local Queue (Public)  | `.\`                 | Stores queue messages in a public queue on the local machine. Other software may have access to this queue.                                                                                                                                                       |
| Remote Queue          | `\\servername\queue` | Stores queue messages on another server. Ensure that the SanteDB Host Process is running as an account which has permission to the remote queue.                                                                                                                  |

## Default Job Manager

The default job manager is the SanteDB service that is responsible for managing system jobs in the iCDR server. These jobs are like CRON jobs and the configuration file should only contain registrations for jobs which need to be run on a schedule.

## Applet Manager

The applet manager configuration panel allows for configuration of the applet repository. The applet repository is the file system location where [SanteDB Applets](../../../developers/extending-santesuite/extending-santedb/applets/) are loaded into the iCDR server context.

![](<../../../.gitbook/assets/image (501).png>)

| Option              | Description                                                                                                                                                                                                                                                    | Example           |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- |
| Applet Directory    | The location on the file system (or on a network share) where applet PAK files should be loaded and stored.                                                                                                                                                    | `\\nas01\applets` |
| Allow Unsigned Code | <p>When TRUE SanteDB will permit the loading of applet PAK files which have no digital signatures attached to them. </p><p>See<a href="../../../developers/santedb-software-publishers/">: SanteDB Software Publishers</a></p>                                 |                   |
| Trusted Publishers  | <p>OBSOLETE</p><p></p><p>Publishers which are not SanteDB Community Publishers should be placed in the Trusted Publishers store of the Microsoft Windows certificate manager on the local machine - alternately they can be added to the Mono trust store.</p> |                   |

## SanteDB Core API

The core API configuration panel allows administrators to change the core behavior of the SanteDB host environment.&#x20;

![](<../../../.gitbook/assets/image (505).png>)

This includes:

* Enabling or disabling core [Daemon services ](../../../developers/extending-santesuite/extending-santedb/server-plugins/implementing-.net-features/daemon-services.md)
* Changing the primary [Passive Service](../../../developers/extending-santesuite/extending-santedb/server-plugins/implementing-.net-features/passive-services.md) assigned to a Service Contract.

{% hint style="info" %}
SanteDB Services are described in the [Service Definitions](../../../developers/server-plugins/implementing-.net-features/service-definitions/) wiki page.
{% endhint %}


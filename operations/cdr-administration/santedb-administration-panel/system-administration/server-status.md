# Server Status

The Server Status page allows system administrators to quickly gather server information for the execution environment. Server status will show:

* The current versions of the SanteDB software running on the server
* The installed plugins and applets installed on the SanteDB dCDR and iCDR
* The applets which have been enabled in the SanteDB server
* The installed services and their current state.

![](<../../../../.gitbook/assets/image (427) (1) (1) (1) (1) (1).png>)

{% hint style="info" %}
Administrators can enable or disable services on the local dCDR instance. This is not recommended on a Windows or Docker instance of SanteDB and is intended primarily for the Disconnected Gateway and Android applications. The setting of these enable/disable flags requires a restart of the host environment to take full effect.
{% endhint %}

The server status page has two tabs:

* Local Server - Showing information related to the dCDR software on which the page has been rendered.
* Realm Server - Showing information related to the iCDR software to which the dCDR is connected.

## Core Information

The core information section of the server status screen shows information related to the server software itself.

![](<../../../../.gitbook/assets/image (434) (1) (1) (1).png>)

## Installed Applets

The installed applets section of the server status screen shows the applets (see: [applets](../../../../developers/extending-santesuite/extending-santedb/applets/ "mention")) which are active and installed on the iCDR or dCDR. Applets are responsible for adding new user interface screens, clinical decision support rules, business rules, etc.

![](<../../../../.gitbook/assets/image (438) (1) (1) (1) (1) (1).png>)

Applets are digitally signed when running in production (unless unsignedApplets are permitted, see: [santedb-software-publishers](../../../../developers/santedb-software-publishers/ "mention")) , the list of applets includes the applet identifier (which appears in logs), the verified publisher, and the version of the applet installed.

## Services

The services panel of the SanteDB iCDR server shows the currently running services which are registered and active on the SanteDB iCDR or dCDR server. On the dCDR users may enable or disable services based on performance or operational requirements.

![](<../../../../.gitbook/assets/image (422) (1) (1).png>)

See: [#service-architecture](../../../../santedb/software-architecture.md#service-architecture "mention") for more information about services.

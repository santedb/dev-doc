# Installing Disconnected Gateway

The SanteDB disconnected gateway is a standalone application which is installed within a clinic and acts as a miniature CDR for a local clinic (on a local area network) and then synchronizes data with a central iCDR server.&#x20;

This deployment pattern is well suited when:

* Several laptops or devices within a clinic need to access SanteDB application functionality
* Users are using thick applications (like OpenMRS or VistA) on a local network and need disconnected functionality&#x20;



See: [Broken link](broken-reference "mention")&#x20;

## Installation on Windows

For Windows based installations, you can obtain the most recent copy of the SanteDB dCG software at the disconnected gateway releases page: [https://github.com/santedb/santedb-dcg/releases](https://github.com/santedb/santedb-dcg/releases) .&#x20;

For other operating systems and environments, you will currently have to manually compile the dCG software from source. This requires the installation and proper setup of the SanteDB SDK as well as compiler tools for Mono. We are working on more installation options.

The installation wizard on the Windows installer simply requires pressing the Next button until the process completes. The installation process on Windows will:

1. Install the software into C:\Program Files\SanteSuite\SanteDB\DCG
2. Register the DCG as a Windows Service to be started automatically
3. Open firewall ports 12100 (HL7v2), 11514 (ATNA), and 9200 (HTTP)
4. Forward you to the configuration tool

After installation is completed, you can configure the service:

![](<../../../../../.gitbook/assets/image (38).png>)

### Installation on Linux and Unix based Operating Systems

{% hint style="info" %}
We're currently writing this section. Please check back soon!
{% endhint %}

## Configuration

SanteDB's dCG software is designed to run remotely on a "server" laptop in a clinic. This server laptop really acts like an entire CDR complete with standards based messaging interfaces, administrative user interfaces, etc. The setup procedure is broken into these stages:

1. Joining the dCG to the central security domain
2. Configuring the Synchronization settings
3. Configuring the local database
4. Configuring local security settings
5. Configuring the standards-based interfaces

{% hint style="info" %}
You must be connected to the internet to perform the initial configuration.
{% endhint %}

### Joining the Security Domain

When you first configure the SanteDB dCG you'll be asked which security domain you'd like to join. There may be several security domains in your jurisdiction depending on different projects, or uses of SanteDB.&#x20;

![](<../../../../../.gitbook/assets/image (73).png>)

The configuration settings are:

* **Device ID:** The name of the device which you are configuring. This should be reflective of where the device is located (for example: HOSPITAL\_A\_HIV\_PROGRAM\_OFFICE)
* **Address:** The address of the domain that you'd like to join
* **Secret Mode:** If you're connecting to a domain which uses a different client secret mode than in the request body you can change it here.
* **Override Application Secret:** By default , the dcg will authenticate itself as org.santedb.disconnectedClient.gateway , if your administrator has changed this you may override the defaults here.
* **Port:** If SanteDB server is running on a different port than the 8080 or 8443 you may enter the correct port
* **Use TLS:** For most production environment you'll check this box to ensure the communication is over TLS.

Once you press **Join Realm** you'll be prompted with an elevation prompt. Enter your username and password for the target domain:

![](<../../../../../.gitbook/assets/image (91).png>)

{% hint style="info" %}
The user account you use MUST be granted the **Create Device Identity** policy permission by the central administrator.&#x20;
{% endhint %}

If successful you'll be welcomed to the domain:

![](<../../../../../.gitbook/assets/image (48).png>)

### Selecting an Application Role

After you've joined the domain you'll be asked to select a role for the gateway. A SanteDB server may have multiple roles (for example: one SanteDB instance may be an MPI, an Immunization Registry and a Master Facility Registry all at the same time). Selecting a role will restrict the local gateway user interface to whatever role has been selected.

You may also select whether you'd like automatic updates to be downloaded when the device is connected to the internet.

### Configuring Synchronization

You can configure the frequency of synchronization and the conflict resolution mechanism on the next screen.&#x20;

![](<../../../../../.gitbook/assets/image (100).png>)

{% hint style="info" %}
If your clinic is never usually connected to the internet, or has limited bandwidth packages. You may select to only manually synchronize with the central server.
{% endhint %}

### Configuring your Subscriptions

When the disconnected gateway is online, it has the opportunity to download a subset of the information from the central server. This is called a subscription. Subscriptions can be to:

* **The Entire Database :** Where the dCG will download a complete copy of the central server (not recommended)
* **Place :** Where the dCG will only download information about patients who live in the specified place.
* **Facility :** Where the dCG can establish a relationship between a patient or event and a facility
* **Identifier :** Where the dCG will only download information which has an identifier from the specified domain.

![](<../../../../../.gitbook/assets/image (84).png>)

### Configure the Local Database

Current SanteDB's dCG only supports SQLite as a storage mechanism, however PostgreSQL and FirebirdSQL are on our roadmap for support. You can configure which database system you'd like to use for your dCG on this screen (for smaller clinics we recommend SQLite).

![](<../../../../../.gitbook/assets/image (82).png>)

### Configure Local Security

Because the dCG operates offline, it must maintain security settings which dictate how it should operate while not connected to the central server. Here you can set:

* The password storage strength
* How long local audits should be retained on the device
* Where the device will operate&#x20;
  * Whether only users assigned to that facility can log in
* Who is the administrative contact for the device

![](<../../../../../.gitbook/assets/image (70).png>)

### Configure Network Settings

The network configuration page allows you to specify parameters about your local network and how it connects to the master server. Here you can specify how heavily you would like to compress traffic (to save bandwidth and time), as well as any proxy settings

![](<../../../../../.gitbook/assets/image (12).png>)

{% hint style="info" %}
Putting the dCG into 2g optimization mode will use LZMA Max compression. This saves quite a bit of bandwidth, however introduces quite a bit of CPU pressure on the dCG (as it requires more computing power to compress traffic). Only use this mode if you are really on a 2g or slow connection where CPU time is less valuable than bandwidth time.
{% endhint %}

### Configure HL7 / LLP Traffic

If you're using a system to communicate with the dCG which uses HL7v2 messaging (such as OpenMRS or VistA) you can setup your LLP traffic settings including the sending facility and device name, and the bind port:

![](<../../../../../.gitbook/assets/image (47).png>)

{% hint style="info" %}
You can change the endpoint to llp://0.0.0.0:12100 to allow external traffic. You can also use sllp:// to indicate you prefer TLS encrypted traffic. You will need to setup the certificate separately however.
{% endhint %}

### Configure the SanteGuard Audit Repository

The dCG comes with a lightweight IHE ATNA compliant audit repository. This is used to track audits against the dCG from local clinic traffic while offline. You can configure the transport and enterprise site ID of the local audit repository:

![](<../../../../../.gitbook/assets/image (27).png>)

### Complete the Installation

After you're done, you can press the Save button. You should be greeted with a notification instructing you to restart the service:

![](<../../../../../.gitbook/assets/image (33).png>)

This is done from the start menu:

![](<../../../../../.gitbook/assets/image (107).png>)

## Confirm Connectivity

After waiting a few seconds, you can login to the main administrative user interface from the local device or from another device on the local network by visiting : http://localhost:9200

![](<../../../../../.gitbook/assets/image (102).png>)

To confirm connectivity, login to the portal and check the synchronization centre status

![](<../../../../../.gitbook/assets/image (63).png>)

{% hint style="info" %}
It is a good idea to have each of the clinic staff login with their accounts during initial setup. This is because the first time a user logs into the dCG they must be connected to the central server for their user profile to be downloaded. Subsequent logins do not require internet access.
{% endhint %}

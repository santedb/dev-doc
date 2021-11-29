# Overall Architecture

This page provides a summary of the SanteDB architecture. A more detailed description of this architecture can be found in the SanteDB Functional Design Specification ([http://santesuite.org/assets/uploads/sdb-arch-1.11.pdf](http://santesuite.org/assets/uploads/sdb-arch-1.11.pdf))

## Overall Architecture

SanteDB is actually made up of several software components which operate together to form the basis of a cohesive digital health infrastructure.&#x20;

![](<../.gitbook/assets/image (122).png>)

## iCDR Server

The iCDR server is the central integrated clinical data repository which is used to coordinate the many connected clients in an implementation. Typically an implementation of SanteDB will only ever have one iCDR instance (or a logical grouping of iCDR servers acting as a single iCDR).

The primary responsibilities of the iCDR are:

* Maintain a master dataset for the entire deployment of SanteDB in a particular health role.
* Facilitate the synchronization and sharing of data between sites within the deployment.
* Integrate with upstream services such as audit repositories, client registries, etc.
* Distribute OTA software updates to connected clients
* Provide a centralized authentication authentication and privacy information distribution point.

## dCDR Clients

The dCDR clients are the disconnected clients which connect to the central iCDR and are typically used by end users. The term dCDR client is used loosely to describe any client which is implemented on the dCDR technology. dCDR clients are deployed in data centers, in clinics, on tablets, etc. A deployment of SanteDB will have multiple dCDR clients.

No matter the implementation, the dCDR clients are primarily responsible for:

* Providing offline access to relevant subsets of data synchronized and replicated from the central iCDR server.
* Caching centralized credentials, and providing local clinic-level authentication
* Serving out the user interface, reports, and other end-user facing elements.
* Providing a federation point for other dCDR instances
* Executing data quality checks, business rules, clinical decision support rules, etc. while the central iCDR server is not available.

### dCDR Android Application

The dCDR Android Application is an implementation of the dCDR services on the Google Android operating system. The dCDR Android application is used whenever tablet or phone users will require access to the SanteDB infrastructure while operating on poor/slow/unavailable cellular internet connections.

The dCDR Android application only exposes the user interface services, offline gateway services such as FHIR, HL7v2, and ATNA are disabled, as is off-host UI access. When the Android host process launches the dCDR service core, it generates a unique secret for that application run, and expects this in the `SDB-Magic` header on all requests.

### dCDR Windows / Linux Applications

The dCDR Windows and Linux applications are self-contained applications which run the SanteDB user interface, and provide a known web-browser component to render them. Like the Android client, these desktop applications disable all API access and generate unique key which is shared between the web-view control and the dCDR services, and is required to access those services.

### dCDR Gateway

The dCDR Gateway is a headless service which implements the dCDR functionality and is intended for use in environments where third party applications (or users in a shared local network) require access to offline functionality.&#x20;

The dCDR gateway exposes FHIR, HL7v2, ATNA, and API calls to any connected client on a local network. The Gateway acts a "mini" SanteDB  iCDR instance, where clients connected on the local network have no knowledge of the overall connectivity of the clinic or environment they're operating within.

{% hint style="info" %}
Care should be taken in planning the local network security environment when using the dCDR gateway.
{% endhint %}

### dCDR Web Portal

The dCDR Web Portal is a specialized dCDR environment which has no offline capability. It is primarily designed to operate as a daemon and to serve out, on the internet, the user interfaces directly connected to the central iCDR. This is the technology used to host the administrative panels, any shared/central infrastructure, etc.


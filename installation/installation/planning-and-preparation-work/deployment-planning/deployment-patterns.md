# Deployment Patterns

There are a variety of ways in which SanteDB can be deployed within your architecture. You can use any of the SanteDB technologies to fill any one of a number of logical roles within your broader e-health strategy.

This page discusses the ways in which SanteDB can be operationalized. It is important to note that these patterns can be mixed, as they leverage common user interface and messaging frameworks.

## Online Only Patterns

### Interoperable Registry

You can deploy many of the SanteDB solutions to operate as a standalone interoperable registry / repository of information. In this deployment pattern, SanteDB is used as a headless repository of information and user-facing interaction is provided by third party applications which connect to SanteDB using any one of the standards supported by SanteDB.

In this deployment, the iCDR interface can be interacted with directly (as shown below) or can operate with an intermediary such as EAI/ESB engine.

This model is most effectively used when leveraging SanteDB within a single organization, or within a single site (like a hospital). You can also leverage this solution over the internet, however it is recommended laying the iCDR infrastructure behind an application firewall or integration services.&#x20;

![SanteDB Operating as an Interoperable Repository/Registry](<../../../../.gitbook/assets/image (140).png>)

Examples of third party applications which may integrate with the iCDR engine may include:

* Logistics Management Information Systems (LMIS)  using the GS1 BMS XML interfaces
* Electronic Medical Records (EMR) Systems using the HL7 Version 2x or HL7 FHIR interfaces
* Personal Health Records (PHR) using the HL7 FHIR interfaces
* Mobile Applications using the HL7 FHIR interfaces
* Any connected system requiring central authentication using the OpenID Connect interface
* Hospital Information Systems (HIS) using the HL7v2 or FHIR interfaces
* Picture Archiving Communication Systems (PACS) using HL7v2 interfaces

### Online Clinical Portal

In this deployment pattern SanteDB's iCDR is bundled with a web portal solution which allows end-users to directly leverage the SanteDB iCDR features using a web browser.&#x20;

This solution is most useful when you have robust internet infrastructure and users can easily access internet based resources.

![](<../../../../.gitbook/assets/image (143).png>)

## Disconnected / Offline Patterns

### Disconnected Registry

In this deployment pattern, SanteDB acts as a disconnected integrator and CDR for solutions that otherwise lack the ability to interoperate in a disconnected way.

&#x20;Here, end users within the clinic use already existing software tooling that they are familiar with. These third party systems communicate with the SanteDB dCDR which has been configured to synchronize with the central iCDR interface using a variety of subscription methods.&#x20;

These clinic systems may require no additional software updates, since the dCDR behaves like a remote endpoint using any one of the standards supported (HL7 v2, HL7 FHIR, etc.). Additionally, the dCDR will execute any business rules which have been configured from the central server while offline. The connection to the iCDR is not necessary to support the operation of the solution.

![](<../../../../.gitbook/assets/image (144).png>)

### Disconnected Clinical Portal

In this deployment, clinic users leverage the dCDR applications to directly interact with the iCDR interface in an online/offline manner, using the end-user portal written in the SanteDB UI framework.&#x20;

![](<../../../../.gitbook/assets/image (145).png>)

The software / portal use in this environment can be:

* Users using laptops/tablets within a single clinic connected to any configured dCDR instance operating in that clinic (for example, over Wi-Fi), the dCDR interface then communicates with the central iCDR.
  * Larger clinics with multiple users and devices
  * Clinics/Hospitals which require a mix of the user portal and third party applications.
* Users using the disconnected portal on an Android tablet or phone. The phone/tablet directly synchronizes its data with the iCDR interface when there is an available internet connection.
  * Community health workers that operate independently offline
  * Small clinics with only one staff member on one device giving care to patients at a time.
* Users using the Windows or Linux user interface. Here the portal operates as a self-contained application on the client and the laptop directly synchronizes with the central iCDR service.
  * Small clinics with only one staff member giving care to patients
* Users connecting using the Android application whereby they may operate in a clinic environment (Wi-Fi against the dCDR) or in the field (offline from the clinic's dCDR). This is a chained synchronization deployment pattern whereby the Android/Windows/Linux app synchronizes against a clinic dCDR, which in turn, synchronizes against the master.&#x20;
  * Larger clinic/hospitals where WI-FI may drop in areas of the clinic
  * Clinics which perform outreach programmes in the community

###




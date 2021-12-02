---
description: Welcome to the SanteSuite Help Portal!
---

# SanteSuite Help Portal

Welcome to the SanteSuite help portal. This portal provides detailed information about the design, configuration and operation of the SanteSuite family of products.&#x20;

{% hint style="info" %}
This site is a living document, and the documentation often changes. If you'd like to participate, documenting SanteDB code or creating help manuals on this site, please let us know!
{% endhint %}

### What is SanteSuite?

SanteSuite is the collection of software solutions built upon the highly scalable and standards compliant SanteDB Clinical Data Repository (CDR). SanteSuite is designed to operate in an "offline-first" fashion, ideal for frequently disconnected, geographically disperse or low-resource environments. SanteSuite products are also platform agnostic and can be run using common open source infrastructure. SanteSuite solutions provide key digital health infrastructure components for regional or national health systems such as Master Patient/Person Index (MPI) (sometimes known as Client Registry), Master Facility Index (MFI), Master Provider Registry (MPR), National Health Identity Management and Immunization Management Systems (IMS).&#x20;

### What is SanteDB?

SanteDB is a general purpose clinical data repository based loosely on the HL7 Reference Information Model (RIM) which we call the Reduced Reference Information Model (RRIM). SanteDB's CDR has four major platform components:

* iCDR - A centralized service for managing data from clinics, tablets, etc. The iCDR provides an implementation of the Reference Information Model (RIM) and offers robust features such as an OAUTH IdP, Audit Repository, versioning, master data management, etc.
* dCDR - We call this one a "baby CDR", and provides disconnected access to SanteDB's functions. The dCDR operates completely on its own and offers almost 75% of the functionality of the iCDR. It is the same implementation of the RIM-based information model, and can operate many of the plugins which are developed for the iCDR.&#x20;
* dCDR Gateway - The **Disconnected Gateway** is a specialized version of the dCDR which combines plugins for HL7v2, ATNA, (and in the future FHIR) and allows clinics who are using third party software such as OpenMRS or OSCAR to leverage dCDR features with standards based interfaces.&#x20;
* Android / Windows / Linux Apps - These applications are built on the dCDR and provide an extensible user interface platform based on HTML5 and JavaScript. By default, AngularJS is the bundled UI framework, however these applications (and applets) may override this and implement their own interfaces to SanteDB's dCDR services.

### Quick Links

* [Architecture Documentation](santedb/architecture.md)
* [Operations Management](operations-1/operations.md)
  * [Installation](installation/installation/)
  * [Knowledgebase](knowledgebase/sdb-kb/)
  * [Fixes & Patches](knowledgebase/fixpatch/)
* [Extending the Platform (SDK)](broken-reference)
* SanteDB Solution Projects
  * [SanteDB Master Patient Index (SanteMPI](product-overview/santesuite-products/master-patient-index-santempi/about-santempi.md))
  * [SanteDB Audit Repository (SanteGuard)](santeguard/introduction.md)
  * [OpenIZ](openiz/about-openiz/)


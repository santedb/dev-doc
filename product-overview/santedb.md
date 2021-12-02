---
description: >-
  This section provides documentation related to the SanteDB Clinical Data
  Repository (CDR) and related technologies.
---

# Introducing SanteDB CDR

### What is SanteDB?

SanteDB is the foundational clinical data repository (CDR) developed by SanteSuite Inc. and leveraged by SanteSuite products. SanteDB is standards-based and highly scalable and is designed for large-scale (regional and national) digital health application deployments.&#x20;

SanteDB forms the core of the SanteSuite product line and provides a robust, secure, repository for modeling and sharing clinical data.

![Figure 1 - SanteDB and SanteSuite](<../.gitbook/assets/image (106).png>)

### Features

Although each of the products built upon SanteDB provide the most clinical value, the platform itself provides the fundamental building blocks required to create disconnected, intelligent health applications. Features of SanteDB include:

* Openness
  * 100% Open Architecture, any application can play in the SanteDB ecosystem.
  * Core platform components and community applets are openly documented and source code provided.
* Private & Secure
  * Privacy and security architecture based on XACML building blocks (though XACML is not used)
  * Authentication of application, device and users
  * Break the glass and permission override supported
  * Full auditing on all platform components (even disconnected clients)
* Intelligent Services
  * Full decision support system provided for expressing care protocols and composing care plans.
  * Business rules can be customized using data triggers
  * Full reporting / ad-hoc warehouse available for custom reports
* Integrated
  * Integrated with a variety of services to assist operationalization
    * Integrated bug submission and tracking with Atlassian JIRA
    * Integrated SMS delivery with Twilio
  * Open interfaces provide 1:1 function access to underlying functionality.
* Interoperable
  * Supports HL7 v2.5 and provides customization interfaces for messages
  * HL7 FHIR STU3 support on select resources
  * Select support for GS1 BMS XML 3.3 (over REST or AS.2)
  * Support for IHE ATNA (RFC 3881 or DICOM)
  * OPENID Connect / OAUTH 2.0 compatible authentication services (password, client\_credential, authorization\_code and refresh grants) with JWT identity tokens

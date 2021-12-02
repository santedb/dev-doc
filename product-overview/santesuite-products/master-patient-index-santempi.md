---
description: This section describes the SanteSuite Master Patient Index SanteMPI
---

# Master Patient Index - SanteMPI

SanteMPI is a next generation, fully functional, open-source and standards-compliant Client Registry that was originally developed to support the Canadian national digital health program beginning in 2006. SanteMPI has been enhanced and refined over decades of investment from governments, private sector companies and non-governmental organizations. SanteMPI has been designed to support the longitudinal management of patient data in jurisdictions around the world and has several proven field deployments in low and middle income countries.

A Master Patient Index (MPI), sometimes called a Client Registry (CR), is a foundational piece of any regional or national health system. Fundamentally, a MPI solution seeks to create a single master list of patients across a jurisdiction and to provide a cross-reference of the various identifiers used by local systems in a region to identify a patient. For example, if a patient is registered in Hospital A as patient number 123 and is registered in Primary Clinic B as patient number 456, a Master Patient Index configured in the region will keep track of these various identifiers and provide a list of them to any system on demand. This enables health care providers to see a "longitudinal view" of a patient, that is, all interactions of the patient with various components of the health care system over time.&#x20;

SantéMPI is a fully functional, national scale, open-source, and standards-compliant Master Patient Index (MPI) / Client Registry (CR) designed for regional and national health system use. SantéMPI was originally developed as a reference implementation to support the Canadian national digital health program administered by Canada Health Infoway ([infoway.ca](http://www.infoway.ca)) beginning in 2006. SantéMPI has been enhanced and refined over decades of investment from various government agencies, private sector companies and non-governmental organizations. SantéMPI has been designed to support the longitudinal management of patient data in jurisdictions around the world and has several proven field deployments in low and middle income countries. SantéMPI has proven to be secure, scalable, reliable, performant, fully featured, standards-compliant, inexpensive and easy to support.

The SantéSuite team that developed SantéMPI have also made significant contributions to the underlying international standards used for MPI/CR systems, including the HL7 v2/v3 and HL7 FHIR standards, the OpenHIE Architecture Specification Client Registry solution, and the IHE patient identity mobile profiles (PIXm and PDQm). These contributions have enhanced the standards to allow for the efficient unique identification of patients even while using low resource mobile devices.

SantéMPI implements all existing interoperable specifications and requirements related to Client Registry in the OpenHIE specification. SantéMPI is fully compliant to operate within a health information exchange (HIE) environment as a Client Registry. SantéMPI has been field tested with millions of successful transactions in multiple jurisdictions, and can operate standalone or as a launching point into a health information exchange. By implementing both modern HL7 FHIR standards and the widely deployed existing legacy HL7v2 standards, SantéMPI provides a platform for integrating existing solutions and future solutions. In this context, SantéMPI has demonstrated integrations with WorldVistA EHR, OpenMRS and OSCAR EMR.

SantéMPI leverages the unique online/offline capability and data architecture of SantéDB by building on our lessons learned developing and implementing the MEDIC CR, especially in low resource environments. SantéMPI meets the stated functional requirements of the OpenHIE Specification for a client registry. Key features of SantéMPI that directly address these requirements include:

Online/Offline Capability – Leveraging SantéDB’s Disconnected Clinical Data Repository (dCDR), SantéMPI is unique in being able to operate offline when and where needed via an online/offline MPI gateway to/from a centrally hosted server or cloud hosted CR service. Clients on the offline gateway can use HL7 v2.5 or HL7 FHIR to perform MPI functions while offline. This offline capability has been proven to be incredibly important in low resource environment where brownouts, blackouts and lack of connectivity situations are commonplace.

Privacy & Security by Design – SantéMPI leverages the SantéDB CDR, which implements a robust privacy and security solution allowing for access control and privacy controls based on role, device, and third-party application via a policy based access control scheme. Security and Privacy are designed into the solution, not bolted on as an afterthought.

Interoperability Standards Support – SantéMPI supports a variety of standards for patient registration including IHE PIX/PDQ (for HL7v2) and HL7 FHIR. It also provides a completely open API for further extension. The SantéSuite team has made significant contributions to health information standards, including being early contributors to HL7 FHIR, as well as authoring the IHE profiles for mobile access to patient identifiers and this platform has previously passed IHE and HL7 Connectathons.

Probabilistic Matching – SantéMPI leverages a customizable record linkage algorithm for detecting whether two or more existing records are the same.

Master Data Management – SantéMPI provides basic master data management functionality, allowing a single record of truth to be synthesized from data submitted from local sources.

Administration Management – SantéMPI provides extensive administrative user interfaces to provide a robust administrative solution.

Mobile Registration App – A mobile registration app has been developed to support search and registration of patients in real time in the field, offering the ability to issue a health identifier to a new client. This app also leverages QR codes as temporary health identifier for easy generation and recognition of a health identifier.

SanteMPI bundles together existing functions of SanteDB (MDM, Matching, Entity Linking, etc.) and exposes additional logic on top of those interfaces to ensure it is a PIX/PDQ compliant product. SanteMPI works in both the SanteDB iCDR and the dCDR, that's right, you can run a mini-MPI offline in a local clinic between systems.

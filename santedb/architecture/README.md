# Architecture

This page provides a summary of the SanteDB architecture. The "source of truth" for this architecture can be found in the SanteDB Functional Design Specification \([http://santesuite.org/assets/uploads/sdb-arch-1.11.pdf](http://santesuite.org/assets/uploads/sdb-arch-1.11.pdf)\)

## Overall Architecture

SanteDB is actually made up of several software components which operate together to form the basis of a cohesive digital health infrastructure. 

![](../../.gitbook/assets/image%20%2842%29.png)

At a high level, the major components of the SanteDB architecture are:

* SanteDB Server \(iCDR\) - The iCDR is the primary platform component of the SanteSuite platform. The SanteDB iCDR is responsible \(at a high level\) for:
  * Maintenance of individuals’ medical records
  * Scheduling and maintenance of medical appointments
  * Forecasting schedules and demand
  * Integration with infrastructural systems such as Logistics Management Information Systems \(LMIS\), Health Management Information Systems \(HMIS\), educational systems, etc.
* SanteDB Disconnected CDR \(dCDR\)  - The dCDR is actually a collection of disconnected solutions which integrate with SanteDB's iCDR. These solutions include:
  * Disconnected Client - Which is a thick client application running on Linux, Windows, or Android which operates offline and hosts a user interface. These applications are designed for end-users to access the user interface in partially connected environments.
  * Disconnected Gateway - Which is actually a server which runs on Windows and Linux and allows multiple devices within a clinic to operate offline. This solution is best used when there is a reliable wireless LAN but no WAN connectivity. The disconnected server supports HL7v2, HL7 FHIR, as well as the sync protocol
* Standards Based Systems - Includes any software which leverages HL7 FHIR, HL7v2 or any of the other standards which SanteDB iCDR or dCDR support.

Upon these base level components a series of products or "solutions" are packaged. These solutions include:

* SanteMPI - A master patient index based on the SanteDB platform
* SanteEMR - A general purpose EMR platform based on the SanteDB platform
* SanteGuard - A general purpose Audit Repository based on the SanteDB platform
* OpenIZ / SanteIMS - An Immunization Management System \(IMS\) 

## .








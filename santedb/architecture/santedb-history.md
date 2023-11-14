---
description: This page describes the history of the SanteDB project.
---

# SanteDB History

SanteDB is the evolution of a reference implementation of the Canadian national digital health platform that originated in a post-secondary institution research lab beginning in 2007. SanteDB was designed with national scale, standards-based digital health applications in mind from the beginning.&#x20;

The SanteDB suite of products incorporates the full functionality of previous research products such as the MEDIC CR client registry and the OpenIZ immunization management system into a deployment-ready, commercially supported package. A brief summary of the evolution of the products is provided in the following section. &#x20;

## Evolution of SanteDB

SanteDB is really an evolution of OpenIZ ([http://openiz.org](http://openiz.org)) which itself was an evolution of the MARC-HI SHR RI. The table below illustrates the relative features of each solution.

| Feature                                          | MARC-HI SHR RI                                         | OpenIZ                                                 | SanteDB iCDR                                                                  |
| ------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ | ----------------------------------------------------------------------------- |
| **Platform Information**                         |                                                        |                                                        |                                                                               |
| Original Release Year                            | 2011                                                   | 2016                                                   | 2019                                                                          |
| MARC-HI Service Core Generation                  | V1                                                     | V2                                                     | N/A                                                                           |
| Technologies / Frameworks                        | .NET 2.0                                               | .NET 4.0, Xamarin, AngularJS 1.5                       | .NET 4.5, Xamarin, AngularJS 1.7                                              |
| Primary Role(s)                                  | Clinical Data Repository (CDR)                         | Electronic Immunization Record (EIR)                   | Clinical Data Repository (CDR)                                                |
| **Deployment / Operationalization**              |                                                        |                                                        |                                                                               |
| Server Environment(s)                            | Windows Server 2003+                                   | Windows Server 2008R2+                                 | Windows Server 2008R2+, Linux, MacOS                                          |
| Client Environments                              |                                                        | Android 4.4+, Windows 7+, Linux, MacOS                 | Android 5.0+, Windows 8+, Linux, MacOS                                        |
| RDBMS Support                                    | PostgreSQL 9.2                                         | PostgreSQL 9.4, SQLite, MSSQL 2008+                    | PostgreSQL 10, FirebirdSQL 3.3, Oracle 11g,   SQLite                          |
| Scale-Out                                        | DB: Streaming Replication, App Server: Round-Robin DNS | DB: Streaming Replication, App Server: Round-Robin DNS | DB: Streaming Replication,  App Server: Round-Robin DNS, Role-Based Scale-out |
| **Information Model**                            |                                                        |                                                        |                                                                               |
| Model                                            | Component Model                                        | HL7 RIM                                                | HL7 RIM                                                                       |
| Encounters                                       |                                                        | X                                                      | X                                                                             |
| Substance Administrations                        | X                                                      | X                                                      | X                                                                             |
| Observations                                     | X                                                      | X                                                      | X                                                                             |
| Clinical Procedures                              | X                                                      |                                                        | X                                                                             |
| Finance (Account, Invoice, etc.)                 |                                                        |                                                        | X                                                                             |
| Patient Administration                           |                                                        | X                                                      | X                                                                             |
| Administrative Units (Place, Organization, etc.) |                                                        | X                                                      | X                                                                             |
| Versioning                                       | X                                                      | X                                                      | X                                                                             |
| **Extendibility**                                |                                                        |                                                        |                                                                               |
| Clinical Decision Support Engine                 |                                                        | X                                                      | X                                                                             |
| Business Rules / Data Triggers                   |                                                        | X                                                      | X                                                                             |
| Plugins (.NET)                                   | X                                                      | X                                                      | X                                                                             |
| **Security / Accountability**                    |                                                        |                                                        |                                                                               |
| ACL Paradigm                                     |                                                        | Policy-Based                                           | Policy Based w/Override                                                       |
| Authentication Methods                           | X509 PKI                                               | OAUTH, HTTP BASIC                                      | OAUTH, HTTP-BASIC, X509 PKI                                                   |
| Auditing                                         | RFC3881                                                | RFC3881, NEMA DICOM                                    | RFC3881, NEMA DICOM, HL7 FHIR STU3                                            |
| **Standards & Interoperability**                 |                                                        |                                                        |                                                                               |
| HL7v2.x                                          | X                                                      | X                                                      | X                                                                             |
| HL7v3                                            | X                                                      |                                                        |                                                                               |
| HL7 CDA                                          | X                                                      |                                                        |                                                                               |
| HL7 FHIR                                         | DSTU1                                                  | DSTU2                                                  | R3                                                                            |
| Other Interfaces                                 |                                                        | GS1 BMS XML 3.3                                        | GS1 BMS XML 3.3                                                               |
| **Optimization / Extra**                         |                                                        |                                                        |                                                                               |
| HTTP Compression                                 | Responses Only                                         | Bi-Directional BZ2, GZ, DF, LZMA                       | Bi-Directional BZ2, GZ, DF, LZMA                                              |
| Data Caching                                     | Memory Cache Only                                      | Memory Cache, REDIS                                    | Memory Cache, REDIS                                                           |
| Matching / Merging Engine                        |                                                        |                                                        | Probabilistic Matching Engine                                                 |
| Master-Data-Model Management                     |                                                        |                                                        | X                                                                             |
| Reporting                                        | 3rd Party                                              | Jasper Reports, ReportR 1.0                            | ReportR 2.0                                                                   |


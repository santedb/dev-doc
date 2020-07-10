# Demonstration Environment

The SanteSuite community partners \(thanks to Fyfe Software Inc. and SanteSuite Inc.\) host a demonstration environment which can be used to illustrate the use of SanteSuite products. These demonstration servers are open to community members and provide a quick way to start writing extensions with the SDK.

Note that demonstration servers may become unavailable at any time and/or may be wiped/reset at anytime.

### Elbonia Ministry Of Health \(SanteMPI\)

The first series of demonstration servers are used to illustrate the SanteMPI services provided by SanteDB. The fake country "Elbonia" \(from the Dilbert comic series, see [https://en.wikipedia.org/wiki/Dilbert\#Elbonia](https://en.wikipedia.org/wiki/Dilbert#Elbonia)\) to illustrate functions typical of a nationally deployed SanteMPI solution. 

#### Central MPI Server

The central MPI server can be accessed by community members at:

Administrative URL: https://elbonia.santesuite.net  
User: demoadmin  
Password: @Elbonia123  
OpenAPI Docs: https://elbonia.santesuite.net:8443/api-docs  
Realm URI: elbonia.santesuite.net \(TLS = on, Port = 8443\)  
HL7v2: sllp://elbonia.santesuite.net:2100  
FHIR: https://elbonia.santesuite.net:8443/fhir  
GS1 AS.2 Endpoint: disabled  
RFC3881 / DICOM SYSLOG: udp://elbonia.santesuite.net:11514

#### Clinic B - OpenMRS 1.9.8

Clinic B is an OpenMRS based clinic illustrating directly integrating a software package with the iCDR \(see [Interoperable Registry pattern](installation/planning-and-preparation-work/deployment-patterns.md#interoperable-registry)\). This clinic is integrated using HL7v2.3.1

URL: https://elbonia\_b\_omrs.santesuite.net/openmrs  
User: demoadmin  
Password: @Elbonia123

#### Clinic C - OpenMRS 2.2 and dCDR

Clinic C is an example of a clinic integrated using the dCDR in an offline manner \(see: [Disconnected Registry pattern](installation/planning-and-preparation-work/deployment-patterns.md#disconnected-registry)\). This clinic is integrated with the dCDR using HL7v2.3.1.

URL: https://elbonia\_c\_omrs.santesuite.net/openmrs-standalone  
User: demoadmin  
Password: @Elbonia123  
  
The disconnected gateway can be accessed using:

URL: https://elbonia\_c\_dcg.santesuite.net  
User: demoadmin  
Password: @Eblonia123




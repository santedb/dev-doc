# Demonstration Environments

The SanteSuite community partner Fyfe Software ([https://fyfesoftware.ca](https://fyfesoftware.ca)) hosts a demonstration environment which can be used to illustrate the use of SanteSuite products. These demonstration servers are open to community members and provide a quick way to start writing extensions with the SDK.

Information about the demonstration servers (and runtime issues) can be sent to [info@fyfesoftware.ca](mailto:info@fyfesoftware.ca) and/or [info@santesuite.com](mailto:info@santesuite.com).

Note that demonstration servers may become unavailable at any time and/or may be wiped/reset at anytime.

## Demonstration Environments

### Sample Ministry of Heatlh (SanteMPI) - Version 3.0

This demonstration server uses Version 3.0 of the SanteDB engine and can be used to evaluate the differences between v2 and v3 of the SanteDB platform.&#x20;

{% hint style="info" %}
The maximum upload size of any files to this server is 256KB. Please ensure that any import data sets being uploaded do not exceed this size.
{% endhint %}

Administrative URL: [https://ncc-1701.santesuite.net/](https://ncc-1701.santesuite.net/)  \
User: demoadmin\
Password: @Training2023\
OpenAPI Docs: [https://ncc-1701.santesuite.net:8443/api-docs](https://ncc-1701.santesuite.net:8443/api-docs)\
Realm URI: ncc-1701.santesuite.net (TLS = on, Port = 8443)\
HL7v2: sllp://ncc-1701.santesuite.net:2100\
FHIR: https://ncc-1701.santesuite.net:8443/fhir\
GS1 AS.2 Endpoint: disabled\
RFC3881 / DICOM SYSLOG: disabled

### Sample Ministry Of Health (SanteMPI) - Version 2.2

The first series of demonstration servers are used to illustrate the SanteMPI services provided by SanteDB. The fake country  to illustrate functions typical of a nationally deployed SanteMPI solution.&#x20;

#### Central MPI Server

The central MPI server can be accessed by community members at:

Administrative URL: [https://demompi.santesuite.net](https://elbonia.santesuite.net)\
User: demoadmin\
Password: @Training123\
OpenAPI Docs: [https://demompi.santesuite.net:8443/api-docs](https://elbonia.santesuite.net:8443/api-docs)\
Realm URI: demompi.santesuite.net (TLS = on, Port = 8443)\
HL7v2: sllp://demompi.santesuite.net:2100\
FHIR: [https://demompi.santesuite.net:8443/fhir](https://elbonia.santesuite.net:8443/fhir)\
GS1 AS.2 Endpoint: disabled\
RFC3881 / DICOM SYSLOG: udp://demompi.santesuite.net:11514

## Use of Environment

### Maintenance Windows

The SanteDB demonstration environments are subject to periodic maintenance for software updates, hardware modifications, etc. Since the community server is operated by volunteers, these windows may shift and/or be unexpected.

If you plan on using the SanteDB community demonstration environments for presentations, or showcases, please contact info@santesuite.com with the date/time you require and our community members will try our level best to ensure that the services are available at that time.

### Storage of Data

The community servers do no store data in an encrypted form at rest. These servers are widely available and any data stored on the demonstration environments is publicly available. It is recommended that these servers be used for demonstration, training, or illustrative purposes only. Our community members are not liable for any data stored on, or disclosed from the community servers. The use of these services are at the user's own risk.

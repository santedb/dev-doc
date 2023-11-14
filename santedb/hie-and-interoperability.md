# HIE & Interoperability

SanteDB is designed with a variety interoperability interfaces and standards, including:

* [HL7 Version 2.3 and Version 2.5 messaging](../developers/service-apis/hl7v2/santedb-hl7v2-implementation.md)
* [HL7 FHIR](../developers/service-apis/hl7-fhir/santedb-fhir-implementation/)&#x20;
* [GS1 BMS 3.3](../developers/service-apis/gs1-bms-xml.md)
* IHE ATNA / UDP
* [OpenID Connect Identity Provider](../developers/service-apis/openid-connect/)
* OpenAPI / Swagger 2.0 Metadata Exchange

Each of these interfaces are enabled/disabled based on the role that SanteDB is operating in. For example, if SanteDB needs to act as an MPI then the GS1 and ATNA interfaces are disabled (along with related user interface platforms).

{% hint style="info" %}
While SanteDB can be integrated into any standards compliant HIE (including OpenHIE), it doesn't require a full HIE infrastructure to operate properly and securely. It can be used as a launch point into a broader e-health infrastructure (i.e. it is possible to launch SanteDB based solutions without an HIE and then build an HIE around it)
{% endhint %}

###

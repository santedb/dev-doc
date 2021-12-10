# HL7 FHIR

SanteDB's HL7 FHIR interfaces are handled through the `SanteDB.Messaging.FHIR.FhirMessageHandler` service and are configured via the `FhirConfigurationSection`. By default the FHIR API endpoint is exposed on the base URL of the server at /fhir.

{% hint style="warning" %}
SanteDB is not a FHIR based CDR however uses a version of the [Reference Information Model](../../../santedb/data-and-information-architecture/conceptual-data-model/) , therefore SanteDB must convert FHIR requests into its own RIM based model. There are several limitations/design decisions. Prior to using the FHIR interface, please review the [SanteDB FHIR Implementation](../../../developers/service-apis/hl7-fhir/santedb-fhir-implementation/) page.
{% endhint %}




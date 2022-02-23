# Developing an Information Architecture

SanteDB is designed to have a common [conceptual-data-model](../../../../santedb/data-and-information-architecture/conceptual-data-model/ "mention"). Because of this, it is important that any jurisdiction adapt this model for their local context, and establish a common understanding of the information which will be captured, shared, and stored in the SanteDB instance.&#x20;

* Develop a minimum dataset for data elements in the CDR, establish common use and definitions, common mappings within the context (i.e. what constitutes a "valid" patient record?)&#x20;
* Identify the identity which can be used in the CDR instance (how are patients identified? how are immunizations identified? etc.) this includes:
  * What are the medical (MRNs, insurance, etc.) and non-medical identification (drivers licenses, citizen identifiers, etc.)
  * Which organizations have the authority to assign/change these identifiers?
  * What are the validation criteria, patterns, expiration, and versioning policies for each?
* Identify standards to be used. It is useful to declare "use FHIR" , however this may not be the best option given the current state of systems. Consider:
  * What information standards are currently used by existing systems?
  * What data elements are easily available in each standard?
* Identify secondary use and indicators for the software. Understand how the data may be aggregated, reported, shared, or compared over time and plan to implement these as reports or measures.

## Contents

{% content-ref url="establishing-minimum-datasets.md" %}
[establishing-minimum-datasets.md](establishing-minimum-datasets.md)
{% endcontent-ref %}

{% content-ref url="developing-privacy-impact-assessments.md" %}
[developing-privacy-impact-assessments.md](developing-privacy-impact-assessments.md)
{% endcontent-ref %}

{% content-ref url="configuring-identity-domains.md" %}
[configuring-identity-domains.md](configuring-identity-domains.md)
{% endcontent-ref %}

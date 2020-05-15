# Conceptual Information Model

The SanteDB conceptual data model is based on several different resources:

* **HL7 Reference Information Model \(RIM\)** forms the basis of the core clinical storage engine. SanteDB's implementation keeps the paradigm of Entities Participating in Acts, however removes many of the complex datatypes.
* **HL7 FHIR** forms the basis for the conceptual data model's extension and tagging capabilities, which are used to extend the SanteDB data model.
* **OpenMRS Concept Dictionary** was used as the basis of SanteDB's concept tables.

## Clinical Data

Clinical data in SanteDB is represented as Entities playing Roles Participating in Acts. This is illustrated in Figure 1.

![Figure 1 - Conceptual Data Model](../../../../.gitbook/assets/image%20%2851%29.png)

* **Entities:** An entity represents a person, place, organization, or thing \(syringe, antigen, vaccine, etc.\). Entities can be related to one another via an entity relationship such as place belonging to an organization or series of materials belonging to a vaccination kit.
* **Roles:** Roles represent a type of part an entity plays. For example, a Person entity may play the role of a provider or a patient.
* **Participations:** Participations are the link between an act and an entity via a role. A participation is used to describe how an entity participates in the carrying out of an act.
* **Acts:** An act represents an action performed. An example of an Act may be an encounter the patient has with a provider to receive a weight or immunization. Acts may be related to one another, for example an encounter may fulfill an appointment, or an observation may be a part of an encounter.

In this context we can represent many different clinical scenarios. In order to make conceptualizing data elements in the SanteDB persistence store easier, much data documentation leverages an information model cards as illustrated in Figure 2.

![Figure 2 - Information Model Cards](../../../../.gitbook/assets/image%20%2871%29.png)

### Templates

SanteDB Acts and Entities can be templated to ease the creation and reuse of common structures. A template is a particular set of rules and pre-set data elements which are used to perform some use case with the underlying base type.

For example, weight and height are two separate types of a QuantityObservation. By creating a “weight” and “height” template, we allow any business processes or user interface elements to understand the rules for a particular entity. It allows software to understand “what kind” of element it is looking at without having to guess based on type/class/mood/determiner/etc.


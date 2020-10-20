# Concept Dictionary

SanteDB's concept dictionary is based heavily on the work done in [OpenMRS' Concept Dictionary](https://wiki.openmrs.org/display/docs/Concept+Dictionary+Basics), the SanteDB concept dictionary is logically made up of four fundamental concepts, described in this page.

![Relationship of Concept Dictionary](../../../../../.gitbook/assets/image%20%28164%29.png)

### Concepts

In SanteDB, a "concept" is a logical construct for representing the idea of something. Concepts are used within the SanteDB core models to represent these ideas on particular attributes. Examples of concepts may be:

* The concept of a "Male", or "Female" 
* The concept of a "Syringe" \(an object used to inject a substance\)
* The concept of "Oral Polio Vaccine" \(an antigen administered orally which protects against polio\)

Concepts are assigned a unique mnemonic \(a human readable term\) and a UUID. Additionally concepts may carry one or more display names. 

#### Concept Relationships 

Concepts can be related to one another via a relationship. The relationship of one concept to another is used to indicate parent/child relationships, specification/generalization, etc. A relationship applies to two concepts and carries a concept relationship classification which can be one of:

| Relationship | Description |
| :--- | :--- |
| Same As | Indicates that concept A is the same as concept B. The two concepts can be considered interchangeable \(i.e. if a system uses concept A and another system queries using concept B, then concept A and B should be considered equal\). |
| Narrower Than | Indicates that concept A represents an idea which is narrower in scope than concept B. For example, a concept of "Diagnosis-YellowFever" would be narrower than "Diagnosis-Fever" |
| Wider Than | Indicates that concept A is a broader idea than concept B. This is the inverse of the Narrower-Than relationship. |
| Negation Of | Indicates that concept A negates concept B.  |
| Inverse Of | Indicates that concept A has the opposite semantic meaning of concept B. |
| Member Of | Indicates that concept A is a member or sub-concept of concept B. For example, a concept for "Ebola" may be a member of the concept "Hemorrhagic Fever". |

### Concept Sets

Concept sets represent a logical grouping of multiple concepts into a single list of related ideas. Concept sets are useful for driving user interface inputs, or allowing the searching/selection of ideas. 

For example, a deployment may use the AdministrativeGender concept set to drive their inputs for selecting gender. Jurisdictions can customize those concepts which are members of this set based on their business requirements. 

{% hint style="info" %}
Some fields in the SanteDB database are bound to concept sets using the ck\_set\_mem\(\) function. This ensures that semantic integrity of data is maintained within the DBMS.
{% endhint %}

### Reference Terms

Reference terms are used for the expression of concept within an external codification system. Reference terms are used to translate concept sets into wire-level codifications of those concepts. This design allows the SanteDB internal data model to maintain integrity with a known internal series of concepts, while mapping those concepts to external code systems which may or may not be subjected to changes \(for example: ICD9, ICD10 and ICD11 can be implemented by simply mapping\).

{% hint style="info" %}
If you're implementing an interface which mandates the use of a separate code list, it is recommended to use the [Concept Repository ](../../../../extending-santedb/server-plugins/service-definitions/repository-services/iconceptrepositoryservice.md)and register your wire-level codes as reference terms.
{% endhint %}


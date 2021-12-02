# Data Dictionary

The data dictionary for entities which store the SanteDB concept dictionary are illustrated below.

![](<../../../../.gitbook/assets/image (163).png>)

### Concept Class

The concept class table stores a complete list of concept classifications.

| Property                         | Type    | Description                                                                                                                   |
| -------------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------- |
| <p>ConceptClassId<br> [1..1]</p> | UUID    | Represents a unique identifier for the concept classification.                                                                |
| <p>Name<br> [1..1]</p>           | VARCHAR | Represents a human readable name for the concept classification. Example: Class Codes                                         |
| <p>Mnemonic<br> [1..1]</p>       | VARCHAR | Represents a system mnemonic for the concept class. The mnemonic does not change even if the human readable Name column does. |

### Concept

The Concept table stores the key data related to a concept. The Concept table represents immutable concept properties that cannot be changed once a concept is created.

| Property                                  | Type | Description                                                                                                                                 |
| ----------------------------------------- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>ConceptId<br> [1..1]</p>               | UUID | A unique identifier for the concept.                                                                                                        |
| <p>IsSystemConcept<br> [1..1] = false</p> | BIT  | An indicator which identifies whether the concept is a system concept (i.e. no further versions can be created, cannot be obsoleted, etc.). |

### Concept Version

The concept version table is used to store mutable properties of a concept. All edits to a concept’s attributes result in a new version being created in the ConceptVersion table.

| Property                                              | Type     | Description                                                                                                                                                                                                           |
| ----------------------------------------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>ConceptVersionId<br> [1..1]</p>                    | UUID     | A unique identifier for the concept version.                                                                                                                                                                          |
| <p>VersionSequenceId<br> [1..1]</p>                   | INT      | A sequence identifier for the version which allows for establishing a time-independent record of version order.                                                                                                       |
| <p>ConceptId</p><p>[1..1]</p>                         | UUID     | The concept to which the version applies.                                                                                                                                                                             |
| <p>CreationTime</p><p>[1..1]</p>                      | DATETIME | The instant in time when the concept version became active (was created). Should default to the current database timestamp.                                                                                           |
| <p>CreatedBy</p><p>[1..1]</p>                         | UUID     | The user who was responsible for the creation of the version, or the system user if the installation process created the concept version.                                                                             |
| <p>ObsoletionTime</p><p>[0..1] ? (> CreationTime)</p> | DATETIME | When present, identifies the time when the concept version did become obsolete. This is used whenever a new version is created, the old version is obsoleted.                                                         |
| <p>ObsoletedBy<br> [0..1] ?(ObsoletionTime)</p>       | UUID     | Indicates the user who was responsible for the obsoletion of the record.                                                                                                                                              |
| <p>ReplacesVersionId<br> [0..1]</p>                   | UUID     | Identifies the concept version that the current version of the concept replaces.                                                                                                                                      |
| <p>ConceptClassId<br> [1..1] = Other</p>              | UUID     | Identifies the classification of the concept as of the version tuple.                                                                                                                                                 |
| <p>Mnemonic<br> [0..1]</p>                            | VARCHAR  | A unique mnemonic used by the system to lookup the concept. The system mnemonic is primarily used for validation purposes where a concept’s identifier does not represent a consistent identifier across deployments. |

### Concept Set

The concept set entity is used to represent logical groupings of concepts which are related in some manner. These typically are used to drive validation (i.e. gender field must be bound to a concept in the gender concept set) or data-entry fields.

| Property                       | Type    | Description                                                                                                   |
| ------------------------------ | ------- | ------------------------------------------------------------------------------------------------------------- |
| <p>ConceptSetId<br> [1..1]</p> | UUID    | A unique identifier for the concept set                                                                       |
| <p>Mnemonic<br> [1..1]</p>     | VARCHAR | The codified name of the concept set (without spaces) used to reference the concept set in queries and paths. |
| <p>Name<br> [1..1]</p>         | VARCHAR | The human readable name of the concept set.                                                                   |
| <p>Url</p><p>[1..1]</p>        | VARCHAR | The URL which defines the concept set.                                                                        |
| <p>Oid</p><p>[1..1]</p>        | VARCHAR | The OID which defines the concept set.                                                                        |

### Concept Name

The concept name table represents a series of human readable names for the concept at a particular version. This facilitates searches as well as translation.

| Property                                              | Type    | Description                                                                                                                                                                   |
| ----------------------------------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>ConceptNameId<br> [1..1]</p>                       | UUID    | A unique identifier for the concept name                                                                                                                                      |
| <p>ConceptId<br> [1..1]</p>                           | UUID    | The concept to which the concept name applies.                                                                                                                                |
| <p>EffectiveVersionSequenceId<br> [1..1]</p>          | UUID    | The version of the concept when the name did become active.                                                                                                                   |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>           | UUID    | The version of the concept when the concept name was obsoleted.                                                                                                               |
| <p>Name<br> [1..1]</p>                                | VARCHAR | The human readable display name for the concept.                                                                                                                              |
| <p>LanguageCode<br> [1..1] ~ ISO639-2 = en</p>        | CHAR    | The ISO639-2 language code for the concept display name.                                                                                                                      |
| <p>PhoneticCode<br> [0..1]</p>                        | VARCHAR | The phonetic code for the display name. This is used for phonetic “sounds-like” searches of concepts.                                                                         |
| <p>PhoneticAlgorithmId<br> [0..1] ?(PhoneticCode)</p> | UUID    | The phonetic algorithm used to generate the phonetic code. This allows deployments to use METAPHONE, SOUNDEX or custom phonetic algorithms appropriate for the language used. |

### Concept Relationship

The concept relationship table is used to link concepts to one another. Concept relationships can represent equivalency between concepts, parent/child relationships, etc.

| Property                                    | Type | Description                                                                              |
| ------------------------------------------- | ---- | ---------------------------------------------------------------------------------------- |
| <p>ConceptRelationshipId<br> [1..1]</p>     | UUID | The unique identifier for the relationship.                                              |
| <p>SourceConceptId<br> [1..1]</p>           | UUID | The concept that represents the source of the relationship.                              |
| <p>TargetConceptId<br> [1..1]</p>           | UUID | The concept which represents the target of the relationship                              |
| <p>EffectiveVerisonId<br> [1..1]</p>        | UUID | Identifies the version of the source concept where the relationship did become active.   |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p> | UUID | Identifies the version of the source concept where the relationship is no longer active. |
| <p>RelationshipTypeId<br> [1..1]</p>        | UUID | Identifies the type of relationship the concepts have.                                   |

### Concept Relationship Type

The concept relationship type represents allowed types of relationships that a concept can have.

| Property                                    | Type    | Description                                                                                        |
| ------------------------------------------- | ------- | -------------------------------------------------------------------------------------------------- |
| <p>ConceptRelationshipTypeId<br> [1..1]</p> | UUID    | The unique identifier for the concept relationship                                                 |
| <p>Name<br> [1..1]</p>                      | VARCHAR | The human readable name of the concept relationship type.                                          |
| <p>Mnemonic<br> [1..1]</p>                  | VARCHAR | An invariant value that represents the type of relationship typically used by software components. |

### Reference Term

A reference term represents a wire level code that can be used to represent the concept.

| Property                          | Type    | Description                                          |
| --------------------------------- | ------- | ---------------------------------------------------- |
| <p>ReferenceTermId<br> [1..1]</p> | UUID    | A unique identifier for the reference term.          |
| <p>CodeSystemId<br> [1..1]</p>    | UUID    | The code system in which the reference term belongs. |
| <p>Mnemonic<br> [1..1]</p>        | VARCHAR | The wire level code mnemonic for the reference term. |

### Concept Reference Term

An associative entity that links a concept to one or more reference terms and indicates the strength of the map.

| Property                                     | Type | Description                                                                                                                         |
| -------------------------------------------- | ---- | ----------------------------------------------------------------------------------------------------------------------------------- |
| <p>ConceptReferenceTermId<br> [1..1]</p>     | UUID | A unique identifier for the concept reference term map                                                                              |
| <p>ConceptId<br> [1..1]</p>                  | UUID | The concept to which the reference term is linked.                                                                                  |
| <p>EffectiveVersionSequenceId<br> [1..1]</p> | UUID | The version of the concept where the reference term map became effective.                                                           |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>  | UUID | The version of the concept where the reference term map became obsolete.                                                            |
| <p>ReferenceTermId<br> [1..1]</p>            | UUID | The reference term which is associated with the concept.                                                                            |
| <p>RelationshipTypeId<br> [1..1]</p>         | UUID | Identifies the relationship (or strength) that the reference term has with the concept. For example: SAME\_AS, NARROWER\_THAN, etc. |

### Code System

The code system table represents a master list of all code systems from which a reference term can be drawn.

| Property                                               | Type     | Description                                                                                                                |
| ------------------------------------------------------ | -------- | -------------------------------------------------------------------------------------------------------------------------- |
| <p>CodeSystemId<br> [1..1]</p>                         | UUID     | A unique identifier for the code system entry.                                                                             |
| <p>Name<br> [1..1]</p>                                 | VARCHAR  | A human readable name for the code system. For example: ICD10                                                              |
| <p>Oid<br> [1..1]</p>                                  | VARCHAR  | The object identifier that identifies the code system in an interoperable manner.                                          |
| <p>Authority</p><p>[1..1]</p>                          | VARCHAR  | The unique assigning authority of the particular code system. Example CVX or SNOMEDCT                                      |
| <p>CreationTime<br> [1..1]</p>                         | DATETIME | The time when the code system entry was created. Default to the current timestamp in the RDBMS.                            |
| <p>CreatedBy<br> [1..1]</p>                            | UUID     | The user that was responsible for the creation of the code system.                                                         |
| <p>ObsoletionTime<br> [0..1] ? (>CreationTime)</p>     | DATETIME | When populated, indicates the time when the code system record is obsolete.                                                |
| <p>ObsoletedBy<br> [0..1] ?(ObsoletionTime)</p>        | UUID     | Identifies the user who was responsible for obsoleting the record.                                                         |
| <p>ObsoletionReason<br> [0..1] ?(ObsoletionReason)</p> | VARCHAR  | The textual description as to why the record was obsoleted.                                                                |
| <p>Url<br> [1..1]</p>                                  | VARCHAR  | A URI that uniquely identifies the code system. This is primarily used when exposing the code system over REST interfaces. |
| <p>Version<br> [0..1]</p>                              | VARCHAR  | A textual description of the version of the code system that this record represents.                                       |

### Reference Term Display Name

Like the ConceptName table, the reference term display name table is used to identify human readable display names associated with the reference term.

| Property                                              | Type     | Description                                                                                                                                                                              |
| ----------------------------------------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>ReferenceTermDisplayNameId<br> [1..1]</p>          | UUID     | The unique identifier for the reference term.                                                                                                                                            |
| <p>ReferenceTermId<br> [1..1]</p>                     | UUID     | The reference term to which the display name applies.                                                                                                                                    |
| <p>LanguageCode<br> [1..1] ~ ISO639-2 = en</p>        | CHAR     | The ISO639-2 language code that identifies the language in which the display name is represented.                                                                                        |
| <p>DisplayName<br> [0..1]</p>                         | VARCHAR  | The human readable name for the reference term.                                                                                                                                          |
| <p>CreationTime<br> [1..1]</p>                        | DATETIME | The time when the display name became active.                                                                                                                                            |
| <p>CreatedBy<br> [1..1]</p>                           | UUID     | Identifies the user that was responsible for the creation of the reference term display name.                                                                                            |
| <p>ObsoletionTime<br> [0..1] ?(>CreationTime)</p>     | DATETIME | When present, identifies the time when the record should no longer be used.                                                                                                              |
| <p>ObsoletedBy<br> [0..1] ?(CreationTime)</p>         | UUID     | Identifies the user that was responsible for obsoleting the display name.                                                                                                                |
| <p>ObsoletionReason<br> [0..1] ?(CreationTime)</p>    | VARCHAR  | A textual description as to why the display name was obsoleted.                                                                                                                          |
| <p>PhoneticCode<br> [0..1]</p>                        | VARCHAR  | Represents a phonetic code that can be used in “sounds-like” queries.                                                                                                                    |
| <p>PhoneticAlgorithmId<br> [0..1] ?(PhoneticCode)</p> | UUID     | Identifies the phonetic algorithm that was used to generate the phonetic code. This allows METAPHONE or SOUNDEX or some other custom language appropriate phonetic algorithm to be used. |


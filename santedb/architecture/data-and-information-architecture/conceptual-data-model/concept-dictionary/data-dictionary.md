# Data Dictionary

The data dictionary for entities which store the SanteDB concept dictionary are illustrated below.

![](../../../../../.gitbook/assets/image%20%28169%29.png)

### Concept Class

The concept class table stores a complete list of concept classifications.

| Property | Type | Description |
| :--- | :--- | :--- |
| ConceptClassId  \[1..1\] | UUID | Represents a unique identifier for the concept classification. |
| Name  \[1..1\] | VARCHAR | Represents a human readable name for the concept classification. Example: Class Codes |
| Mnemonic  \[1..1\] | VARCHAR | Represents a system mnemonic for the concept class. The mnemonic does not change even if the human readable Name column does. |

### Concept

The Concept table stores the key data related to a concept. The Concept table represents immutable concept properties that cannot be changed once a concept is created.

| Property | Type | Description |
| :--- | :--- | :--- |
| ConceptId  \[1..1\] | UUID | A unique identifier for the concept. |
| IsSystemConcept  \[1..1\] = false | BIT | An indicator which identifies whether the concept is a system concept \(i.e. no further versions can be created, cannot be obsoleted, etc.\). |

### Concept Version

The concept version table is used to store mutable properties of a concept. All edits to a concept’s attributes result in a new version being created in the ConceptVersion table.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Property</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ConceptVersionId
        <br />[1..1]</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">A unique identifier for the concept version.</td>
    </tr>
    <tr>
      <td style="text-align:left">VersionSequenceId
        <br />[1..1]</td>
      <td style="text-align:left">INT</td>
      <td style="text-align:left">A sequence identifier for the version which allows for establishing a
        time-independent record of version order.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>ConceptId</p>
        <p>[1..1]</p>
      </td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">The concept to which the version applies.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CreationTime</p>
        <p>[1..1]</p>
      </td>
      <td style="text-align:left">DATETIME</td>
      <td style="text-align:left">The instant in time when the concept version became active (was created).
        Should default to the current database timestamp.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>CreatedBy</p>
        <p>[1..1]</p>
      </td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">The user who was responsible for the creation of the version, or the system
        user if the installation process created the concept version.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>ObsoletionTime</p>
        <p>[0..1] ? (&gt; CreationTime)</p>
      </td>
      <td style="text-align:left">DATETIME</td>
      <td style="text-align:left">When present, identifies the time when the concept version did become
        obsolete. This is used whenever a new version is created, the old version
        is obsoleted.</td>
    </tr>
    <tr>
      <td style="text-align:left">ObsoletedBy
        <br />[0..1] ?(ObsoletionTime)</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Indicates the user who was responsible for the obsoletion of the record.</td>
    </tr>
    <tr>
      <td style="text-align:left">ReplacesVersionId
        <br />[0..1]</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Identifies the concept version that the current version of the concept
        replaces.</td>
    </tr>
    <tr>
      <td style="text-align:left">ConceptClassId
        <br />[1..1] = Other</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Identifies the classification of the concept as of the version tuple.</td>
    </tr>
    <tr>
      <td style="text-align:left">Mnemonic
        <br />[0..1]</td>
      <td style="text-align:left">VARCHAR</td>
      <td style="text-align:left">A unique mnemonic used by the system to lookup the concept. The system
        mnemonic is primarily used for validation purposes where a concept&#x2019;s
        identifier does not represent a consistent identifier across deployments.</td>
    </tr>
  </tbody>
</table>

### Concept Name

The concept name table represents a series of human readable names for the concept at a particular version. This facilitates searches as well as translation.

| Property | Type | Description |
| :--- | :--- | :--- |
| ConceptNameId  \[1..1\] | UUID | A unique identifier for the concept name |
| ConceptId  \[1..1\] | UUID | The concept to which the concept name applies. |
| EffectiveVersionSequenceId  \[1..1\] | UUID | The version of the concept when the name did become active. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | The version of the concept when the concept name was obsoleted. |
| Name  \[1..1\] | VARCHAR | The human readable display name for the concept. |
| LanguageCode  \[1..1\] ~ ISO639-2 = en | CHAR | The ISO639-2 language code for the concept display name. |
| PhoneticCode  \[0..1\] | VARCHAR | The phonetic code for the display name. This is used for phonetic “sounds-like” searches of concepts. |
| PhoneticAlgorithmId  \[0..1\] ?\(PhoneticCode\) | UUID | The phonetic algorithm used to generate the phonetic code. This allows deployments to use METAPHONE, SOUNDEX or custom phonetic algorithms appropriate for the language used. |

### Concept Relationship

The concept relationship table is used to link concepts to one another. Concept relationships can represent equivalency between concepts, parent/child relationships, etc.

| Property | Type | Description |
| :--- | :--- | :--- |
| ConceptRelationshipId  \[1..1\] | UUID | The unique identifier for the relationship. |
| SourceConceptId  \[1..1\] | UUID | The concept that represents the source of the relationship. |
| TargetConceptId  \[1..1\] | UUID | The concept which represents the target of the relationship |
| EffectiveVerisonId  \[1..1\] | UUID | Identifies the version of the source concept where the relationship did become active. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | Identifies the version of the source concept where the relationship is no longer active. |
| RelationshipTypeId  \[1..1\] | UUID | Identifies the type of relationship the concepts have. |

### Concept Relationship Type

The concept relationship type represents allowed types of relationships that a concept can have.

| Property | Type | Description |
| :--- | :--- | :--- |
| ConceptRelationshipTypeId  \[1..1\] | UUID | The unique identifier for the concept relationship |
| Name  \[1..1\] | VARCHAR | The human readable name of the concept relationship type. |
| Mnemonic  \[1..1\] | VARCHAR | An invariant value that represents the type of relationship typically used by software components. |

### Reference Term

A reference term represents a wire level code that can be used to represent the concept.

| Property | Type | Description |
| :--- | :--- | :--- |
| ReferenceTermId  \[1..1\] | UUID | A unique identifier for the reference term. |
| CodeSystemId  \[1..1\] | UUID | The code system in which the reference term belongs. |
| Mnemonic  \[1..1\] | VARCHAR | The wire level code mnemonic for the reference term. |

### Concept Reference Term

An associative entity that links a concept to one or more reference terms and indicates the strength of the map.

| Property | Type | Description |
| :--- | :--- | :--- |
| ConceptReferenceTermId  \[1..1\] | UUID | A unique identifier for the concept reference term map |
| ConceptId  \[1..1\] | UUID | The concept to which the reference term is linked. |
| EffectiveVersionSequenceId  \[1..1\] | UUID | The version of the concept where the reference term map became effective. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | The version of the concept where the reference term map became obsolete. |
| ReferenceTermId  \[1..1\] | UUID | The reference term which is associated with the concept. |
| RelationshipTypeId  \[1..1\] | UUID | Identifies the relationship \(or strength\) that the reference term has with the concept. For example: SAME\_AS, NARROWER\_THAN, etc. |

### Code System

The code system table represents a master list of all code systems from which a reference term can be drawn.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Property</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CodeSystemId
        <br />[1..1]</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">A unique identifier for the code system entry.</td>
    </tr>
    <tr>
      <td style="text-align:left">Name
        <br />[1..1]</td>
      <td style="text-align:left">VARCHAR</td>
      <td style="text-align:left">A human readable name for the code system. For example: ICD10</td>
    </tr>
    <tr>
      <td style="text-align:left">Oid
        <br />[1..1]</td>
      <td style="text-align:left">VARCHAR</td>
      <td style="text-align:left">The object identifier that identifies the code system in an interoperable
        manner.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Authority</p>
        <p>[1..1]</p>
      </td>
      <td style="text-align:left">VARCHAR</td>
      <td style="text-align:left">The unique assigning authority of the particular code system. Example
        CVX or SNOMEDCT</td>
    </tr>
    <tr>
      <td style="text-align:left">CreationTime
        <br />[1..1]</td>
      <td style="text-align:left">DATETIME</td>
      <td style="text-align:left">The time when the code system entry was created. Default to the current
        timestamp in the RDBMS.</td>
    </tr>
    <tr>
      <td style="text-align:left">CreatedBy
        <br />[1..1]</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">The user that was responsible for the creation of the code system.</td>
    </tr>
    <tr>
      <td style="text-align:left">ObsoletionTime
        <br />[0..1] ? (&gt;CreationTime)</td>
      <td style="text-align:left">DATETIME</td>
      <td style="text-align:left">When populated, indicates the time when the code system record is obsolete.</td>
    </tr>
    <tr>
      <td style="text-align:left">ObsoletedBy
        <br />[0..1] ?(ObsoletionTime)</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Identifies the user who was responsible for obsoleting the record.</td>
    </tr>
    <tr>
      <td style="text-align:left">ObsoletionReason
        <br />[0..1] ?(ObsoletionReason)</td>
      <td style="text-align:left">VARCHAR</td>
      <td style="text-align:left">The textual description as to why the record was obsoleted.</td>
    </tr>
    <tr>
      <td style="text-align:left">Url
        <br />[1..1]</td>
      <td style="text-align:left">VARCHAR</td>
      <td style="text-align:left">A URI that uniquely identifies the code system. This is primarily used
        when exposing the code system over REST interfaces.</td>
    </tr>
    <tr>
      <td style="text-align:left">Version
        <br />[0..1]</td>
      <td style="text-align:left">VARCHAR</td>
      <td style="text-align:left">A textual description of the version of the code system that this record
        represents.</td>
    </tr>
  </tbody>
</table>

### Reference Term Display Name

Like the ConceptName table, the reference term display name table is used to identify human readable display names associated with the reference term.

| Property | Type | Description |
| :--- | :--- | :--- |
| ReferenceTermDisplayNameId  \[1..1\] | UUID | The unique identifier for the reference term. |
| ReferenceTermId  \[1..1\] | UUID | The reference term to which the display name applies. |
| LanguageCode  \[1..1\] ~ ISO639-2 = en | CHAR | The ISO639-2 language code that identifies the language in which the display name is represented. |
| DisplayName  \[0..1\] | VARCHAR | The human readable name for the reference term. |
| CreationTime  \[1..1\] | DATETIME | The time when the display name became active. |
| CreatedBy  \[1..1\] | UUID | Identifies the user that was responsible for the creation of the reference term display name. |
| ObsoletionTime  \[0..1\] ?\(&gt;CreationTime\) | DATETIME | When present, identifies the time when the record should no longer be used. |
| ObsoletedBy  \[0..1\] ?\(CreationTime\) | UUID | Identifies the user that was responsible for obsoleting the display name. |
| ObsoletionReason  \[0..1\] ?\(CreationTime\) | VARCHAR | A textual description as to why the display name was obsoleted. |
| PhoneticCode  \[0..1\] | VARCHAR | Represents a phonetic code that can be used in “sounds-like” queries. |
| PhoneticAlgorithmId  \[0..1\] ?\(PhoneticCode\) | UUID | Identifies the phonetic algorithm that was used to generate the phonetic code. This allows METAPHONE or SOUNDEX or some other custom language appropriate phonetic algorithm to be used. |




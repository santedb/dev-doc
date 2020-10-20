# Data Dictionary

The act data model describes the tables and fields required for the tracking of acts in the SanteDB logical model.

![](../../../../../.gitbook/assets/image%20%28170%29.png)

### Act Entity

The act table is represents the immutable attributes of an act.

| Column | Type | Description |
| :--- | :--- | :--- |
| ActId  \[1..1\] | UUID | A unique identifier for the act. |
| TemplateDefinitionId  \[1..1\] | UUID | Identifies the template definition that the particular act implements. |
| ClassConceptId  \[1..1\] ~ ActClass | UUID | Identifies a concept that classifies the act. This determines the type of act, for example an Observation, PatientEncounter, etc. |
| MoodConceptId  \[1..1\] ~ ActMood | UUID | Identifies the mood, or method of the act’s performance. |

### ActTag Entity

A table for storing tags related to acts. A tag represents a version independent piece of data attached to a tag.

| Column | Type | Description |
| :--- | :--- | :--- |
| ActTagId  \[1..1\] | UUID | A unique identifier for the tag. |
| ActId  \[1..1\] | UUID | Identifies the act to which the tag is applied. |
| Key  \[1..1\] | VARCHAR | A unique key identifier for the type of tag. A tag’s key is used to convey the type of data. |
| Value  \[1..1\] | VARBINARY | Contains the binary data of the tag. |
| CreationTime  \[1..1\] | DATETIME | Identifies the time when the tag became active, or was created. |
| CreatedBy  \[1..1\] | UUID | Identifies the user that was responsible for the creation of the tag. |
| ObsoletionTime  \[0..1\] ?\(&gt;CreationTime\) | DATETIME | When present, identifies the time that the tag data is no longer valid. |
| ObsoletedBy  \[0..1\] ?\(ObsoletionTime\) | UUID | Identifies the user who obsoleted the act tag. |

### ActVersion Entity

<table>
  <thead>
    <tr>
      <th style="text-align:left">Column</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ActVersionId
        <br />[1..1]</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">A unique identifier for the version.</td>
    </tr>
    <tr>
      <td style="text-align:left">VersionSequenceId
        <br />[1..1]</td>
      <td style="text-align:left">INT</td>
      <td style="text-align:left">A sequence identifier for the version which allows for a time independent
        mechanism for establishing version order.</td>
    </tr>
    <tr>
      <td style="text-align:left">ActId
        <br />[1..1]</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Identifies the act to which the version data applies.</td>
    </tr>
    <tr>
      <td style="text-align:left">CreationTime
        <br />[1..1]</td>
      <td style="text-align:left">DATETIME</td>
      <td style="text-align:left">Identifies the time when the act version became active (was created)</td>
    </tr>
    <tr>
      <td style="text-align:left">CreatedBy
        <br />[1..1]</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Identifies the user that was responsible for creating the version.</td>
    </tr>
    <tr>
      <td style="text-align:left">ObsoletionTime
        <br />[0..1] ? (&gt;CreationTime)</td>
      <td style="text-align:left">DATETIME</td>
      <td style="text-align:left">When present, identifies the time when the version of the act is no longer
        active.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>ObsoletedBy</p>
        <p>[0..1] ?(ObsoletionTime)</p>
      </td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Identifies the user who was responsible for the obsoletion of the version.</td>
    </tr>
    <tr>
      <td style="text-align:left">NegationInd
        <br />[1..1] = false</td>
      <td style="text-align:left">BIT</td>
      <td style="text-align:left">When present, indicates that the act&#x2019;s value is not true. For example,
        when attempting to convey that a vaccine was not given, the negationInd
        would be set to true.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>TypeConceptId</p>
        <p>[0..1]</p>
      </td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Identifies the type of act. This is a type that is a subclass within the
        major classification. For example, if the class is a substance administration,
        the type concept may represent an Immunization.</td>
    </tr>
    <tr>
      <td style="text-align:left">StatusConceptId
        <br />[1..1] ~ActStatus</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Identifies the status of the act as of the current version.</td>
    </tr>
    <tr>
      <td style="text-align:left">ActTime
        <br />[0..1] ?(ActTime | ActStartTime | ActStopTime)</td>
      <td style="text-align:left">DATETIME</td>
      <td style="text-align:left">Identifies the time that the act did occurred, should occur.</td>
    </tr>
    <tr>
      <td style="text-align:left">ActStartTime
        <br />[0..1] ?(ActTime | ActStartTime | ActStopTime)</td>
      <td style="text-align:left">DATETIME</td>
      <td style="text-align:left">Identifies the start time of the act.</td>
    </tr>
    <tr>
      <td style="text-align:left">ActStopTime
        <br />[0..1] ?(ActTime | ActStartTime | ActStopTime)</td>
      <td style="text-align:left">DATETIME</td>
      <td style="text-align:left">Identifies the stop time of the act.</td>
    </tr>
  </tbody>
</table>

### ActRelationship Entity

The act relationship table is used to track the relationship of acts to one another.

| Column | Type | Description |
| :--- | :--- | :--- |
| ActRelationshipId  \[1..1\] | UUID | Uniquely identifies the act relationship. |
| SourceActId  \[1..1\] | UUID | Identifies the source act of the relationship. |
| TargetActId  \[1..1\] | UUID | Identifies the target act of the relationship. |
| EffectiveVersionSequenceId  \[1..1\] | UUID | Identifies the version of the source act where this relationship did become active. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | Identifies the version of the source act where this relationship is no longer active. |
| RelationshipTypeConceptId  \[1..1\] ~ActRelationshipType | UUID | Identifies the type of relationship that the two acts have to one another. |

### ActParticipation Entity

The ActParticipation table is used to track how entities participate in a particular act.

| Column | Type | Description |
| :--- | :--- | :--- |
| ActParticipationId  \[1..1\] | UUID | Uniquely identifies the act participation. |
| ActId  \[1..1\] | UUID | Identifies the act that the participation is for. |
| EffectiveVersionSequenceId  \[1..1\] | UUID | Identifies the version of the act when the participation is active. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | When present, identifies the version of the act when the participation is no longer active. |
| ParticipationRoleConceptId  \[1..1\] ~ActParticipationType | UUID | Qualifies what role the entity played in the carrying out of the act. |
| Quantity  \[1..1\] = 1 | INT | Identifies the number of entities that are included in the playing of the role. |

### ActIdentifier Entity

The act identifier table is used to store alternate identifiers for the act. This may include vaccine event identifiers, external order identifiers, etc.

| Column | Type | Description |
| :--- | :--- | :--- |
| ActIdentifierId  \[1..1\] | UUID | Uniquely identifies the alternate act identifier. |
| IdentifierTypeId  \[0..1\] | UUID | Identifies the type of identifier this particular identifier instance represents \(order \#, etc.\) |
| AssigningAuthorityId  \[1..1\] | UUID | Identifies the authority that assigned the identifier. |
| IdentifierValue  \[1..1\] | VARCHAR | The actual external identifier value. |
| EffectiveVersionSequenceId  \[1..1\] | UUID | Identifies the version of the act where the alternate identifier became active. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | When present, identifies the version of the act whereby the alternate identifier is no longer active. |

### ActExtension Entity

The act extension table is used to store extensions attached to acts.

| Column | Type | Description |
| :--- | :--- | :--- |
| ActExtensionId  \[1..1\] | UUID | A unique identifier for the act extension. |
| ExtensionTypeId  \[1..1\] | UUID | Identifies the type of extension represented. This includes information on how the extension should be serialized to/from the ExtensionValue column. |
| ExtensionValue  \[1..1\] | VARBINARY | Carries the value of the extension. |
| ExtensionDisplay  \[1..1\] | VARCHAR | A human comprehendible display value for the extension. |
| EffectiveVersionSequenceId  \[1..1\] | UUID | Indicates the version of the act where this extension became active. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | When present, indicates the version of the act where the extension is no longer active. |

### Observation Entity

The observation table is used to store extended values related to observation act types.

| Column | Type | Description |
| :--- | :--- | :--- |
| ActVersionId  \[1..1\] | UUID | Identifies the act version to which this extended data applies. |
| InterpretationConceptId  \[0..1\] ~ActInterpretation | UUID | Identifies the concept that represents the interpretation of the observation. |

### QuantityObservation Entity

The quantity observation table is used to store extended information related to the observations that carry quantified values.

| Column | Type | Description |
| :--- | :--- | :--- |
| ActVersionId  \[1..1\] | UUID | Identifies the observation act version to which the quantified observation data applies. |
| Quantity  \[1..1\] | DECIMAL | A decimal value that contains the value of the observation quantity. |
| QuantityPrecision  \[1..1\] | INT | Identifies the precision of the Quantity field. |
| UnitOfMeasureConceptId  \[1..1\] ~UnitOfMeasure | UUID | Identifies the concept that identifies the units of measurement. |

### TextObservation Entity

The text observation table is used to store additional information related to a text valued observation.

| Column | Type | Description |
| :--- | :--- | :--- |
| ActVersionId  \[1..1\] | UUID | Identifies the observation version id that this text observation data is attached to. |
| TextValue  \[1..1\] | TEXT | A textual field that contains the observation data. |

### CodedObservation Entity

The coded observation table is used to store additional data related to observations that are coded. Problems and Allergies would qualify as coded observations.

| Column | Type | Description |
| :--- | :--- | :--- |
| ActVersionId  \[1..1\] | UUID | Identifies the version of the observation that this coded observation value data applies. |
| ConceptValueId  \[1..1\] | UUID | Identifies the concept that represents the value of observation. |

### SubstanceAdministration Entity

The substance administration table is used to store data related to substance administrations to a patient. This include vaccines or any type of Epupin injections for

| Column | Type | Description |
| :--- | :--- | :--- |
| ActVersionId  \[1..1\] | UUID | Identifies the act version to which the substance administration data applies. |
| RouteConceptId  \[0..1\] ~RouteConcept | UUID | Identifies the concept that describes the route that was taken to administer the substance. This may be drawn from the default route if not supplied. |
| DoseQuantity  \[1..1\] | DECIMAL | Identifies the dosage that was given to the patient. |
| DoseQuantityPrecision  \[1..1\] | INT | Identifies the precision of the dose quantity. |
| DoseUnitConceptId  \[1..1\] ~UnitOfMeasure | INT | Identifies the dose unit of measure that was given to the patient. |
| SequenceId  \[0..1\] | INT | Identifies the sequence of this dose if it is a part of a sequence of doses. |

### PatientEncounter Entity

The patient encounter table is used to store additional data related to an act that represents a patient encounter.

| Column | Type | Description |
| :--- | :--- | :--- |
| ActVersionId  \[1..1\] | UUID | Identifies the act to which the extended patient encounter data applies. |
| DischargeDispositionConceptId  \[0..1\] ~DischargeDisposition | UUID | Identifies the disposition in which the patient left the encounter. |

### ActNote Entity

The act note table is used to store notes associated with an act.

| Column | Type | Description |
| :--- | :--- | :--- |
| ActNoteId  \[1..1\] | UUID | A unique identifier for the note. |
| EffectiveVersionSequenceId  \[1..1\] | UUID | The version whereby the note became effective |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | When populated, indicates the version of the act where the note is no longer active. |
| AuthorEntityId  \[1..1\] | UUID | The identifier of the entity that wrote the note. |
| NoteText  \[1..1\] | TEXT | The textual content of the note. |

### Procedure Entity

Used to track acts which alter the physical state of an entity \(i.e. surgeries, etc.\)

| Column | Type | Description |
| :--- | :--- | :--- |
| ActVersionId  \[1..1\] | UUID | Points to the version of the Act which this procedure is describing. |
| MethodCodeId  \[0..1\] ~ProcedureTechniqueCode | UUID | Identifies the formal method for performing the procedure. |
| ApproachSiteCodeId  \[0..1\] ~BodySiteOrSystemCode | UUID | Identifies the manner in which the target site was approached for the procedure. |
| TargetSiteCodeId  \[0..1\] ~BodySiteOrSystemCode | UUID | Identifies the body system/part which was the target of the procedure. |


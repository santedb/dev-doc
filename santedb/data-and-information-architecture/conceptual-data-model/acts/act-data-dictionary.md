# Data Dictionary

The act data model describes the tables and fields required for the tracking of acts in the SanteDB logical model.

![](<../../../../.gitbook/assets/image (256).png>)

### Act Entity

The act table is represents the immutable attributes of an act.

| Column                                      | Type | Description                                                                                                                       |
| ------------------------------------------- | ---- | --------------------------------------------------------------------------------------------------------------------------------- |
| <p>ActId<br> [1..1]</p>                     | UUID | A unique identifier for the act.                                                                                                  |
| <p>TemplateDefinitionId<br> [1..1]</p>      | UUID | Identifies the template definition that the particular act implements.                                                            |
| <p>ClassConceptId<br> [1..1] ~ ActClass</p> | UUID | Identifies a concept that classifies the act. This determines the type of act, for example an Observation, PatientEncounter, etc. |
| <p>MoodConceptId<br> [1..1] ~ ActMood</p>   | UUID | Identifies the mood, or method of the act’s performance.                                                                          |

### ActTag Entity

A table for storing tags related to acts. A tag represents a version independent piece of data attached to a tag.

| Column                                            | Type      | Description                                                                                  |
| ------------------------------------------------- | --------- | -------------------------------------------------------------------------------------------- |
| <p>ActTagId<br> [1..1]</p>                        | UUID      | A unique identifier for the tag.                                                             |
| <p>ActId<br> [1..1]</p>                           | UUID      | Identifies the act to which the tag is applied.                                              |
| <p>Key<br> [1..1]</p>                             | VARCHAR   | A unique key identifier for the type of tag. A tag’s key is used to convey the type of data. |
| <p>Value<br> [1..1]</p>                           | VARBINARY | Contains the binary data of the tag.                                                         |
| <p>CreationTime<br> [1..1]</p>                    | DATETIME  | Identifies the time when the tag became active, or was created.                              |
| <p>CreatedBy<br> [1..1]</p>                       | UUID      | Identifies the user that was responsible for the creation of the tag.                        |
| <p>ObsoletionTime<br> [0..1] ?(>CreationTime)</p> | DATETIME  | When present, identifies the time that the tag data is no longer valid.                      |
| <p>ObsoletedBy<br> [0..1] ?(ObsoletionTime)</p>   | UUID      | Identifies the user who obsoleted the act tag.                                               |

### ActVersion Entity

| Column                                                                 | Type     | Description                                                                                                                                                                                             |
| ---------------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>ActVersionId<br> [1..1]</p>                                         | UUID     | A unique identifier for the version.                                                                                                                                                                    |
| <p>VersionSequenceId<br> [1..1]</p>                                    | INT      | A sequence identifier for the version which allows for a time independent mechanism for establishing version order.                                                                                     |
| <p>ActId<br> [1..1]</p>                                                | UUID     | Identifies the act to which the version data applies.                                                                                                                                                   |
| <p>CreationTime<br> [1..1]</p>                                         | DATETIME | Identifies the time when the act version became active (was created)                                                                                                                                    |
| <p>CreatedBy<br> [1..1]</p>                                            | UUID     | Identifies the user that was responsible for creating the version.                                                                                                                                      |
| <p>ObsoletionTime<br> [0..1] ? (>CreationTime)</p>                     | DATETIME | When present, identifies the time when the version of the act is no longer active.                                                                                                                      |
| <p>ObsoletedBy</p><p>[0..1] ?(ObsoletionTime)</p>                      | UUID     | Identifies the user who was responsible for the obsoletion of the version.                                                                                                                              |
| <p>NegationInd<br> [1..1] = false</p>                                  | BIT      | When present, indicates that the act’s value is not true. For example, when attempting to convey that a vaccine was not given, the negationInd would be set to true.                                    |
| <p>TypeConceptId</p><p>[0..1]</p>                                      | UUID     | Identifies the type of act. This is a type that is a subclass within the major classification. For example, if the class is a substance administration, the type concept may represent an Immunization. |
| <p>StatusConceptId<br> [1..1] ~ActStatus</p>                           | UUID     | Identifies the status of the act as of the current version.                                                                                                                                             |
| <p>ActTime<br> [0..1] ?(ActTime | ActStartTime | ActStopTime)</p>      | DATETIME | Identifies the time that the act did occurred, should occur.                                                                                                                                            |
| <p>ActStartTime<br> [0..1] ?(ActTime | ActStartTime | ActStopTime)</p> | DATETIME | Identifies the start time of the act.                                                                                                                                                                   |
| <p>ActStopTime<br> [0..1] ?(ActTime | ActStartTime | ActStopTime)</p>  | DATETIME | Identifies the stop time of the act.                                                                                                                                                                    |

### ActRelationship Entity

The act relationship table is used to track the relationship of acts to one another.

| Column                                                           | Type | Description                                                                           |
| ---------------------------------------------------------------- | ---- | ------------------------------------------------------------------------------------- |
| <p>ActRelationshipId<br> [1..1]</p>                              | UUID | Uniquely identifies the act relationship.                                             |
| <p>SourceActId<br> [1..1]</p>                                    | UUID | Identifies the source act of the relationship.                                        |
| <p>TargetActId<br> [1..1]</p>                                    | UUID | Identifies the target act of the relationship.                                        |
| <p>EffectiveVersionSequenceId<br> [1..1]</p>                     | UUID | Identifies the version of the source act where this relationship did become active.   |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>                      | UUID | Identifies the version of the source act where this relationship is no longer active. |
| <p>RelationshipTypeConceptId<br> [1..1] ~ActRelationshipType</p> | UUID | Identifies the type of relationship that the two acts have to one another.            |

### ActParticipation Entity

The ActParticipation table is used to track how entities participate in a particular act.

| Column                                                             | Type | Description                                                                                 |
| ------------------------------------------------------------------ | ---- | ------------------------------------------------------------------------------------------- |
| <p>ActParticipationId<br> [1..1]</p>                               | UUID | Uniquely identifies the act participation.                                                  |
| <p>ActId<br> [1..1]</p>                                            | UUID | Identifies the act that the participation is for.                                           |
| <p>EffectiveVersionSequenceId<br> [1..1]</p>                       | UUID | Identifies the version of the act when the participation is active.                         |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>                        | UUID | When present, identifies the version of the act when the participation is no longer active. |
| <p>ParticipationRoleConceptId<br> [1..1] ~ActParticipationType</p> | UUID | Qualifies what role the entity played in the carrying out of the act.                       |
| <p>Quantity<br> [1..1] = 1</p>                                     | INT  | Identifies the number of entities that are included in the playing of the role.             |

### ActIdentifier Entity

The act identifier table is used to store alternate identifiers for the act. This may include vaccine event identifiers, external order identifiers, etc.

| Column                                       | Type    | Description                                                                                           |
| -------------------------------------------- | ------- | ----------------------------------------------------------------------------------------------------- |
| <p>ActIdentifierId<br> [1..1]</p>            | UUID    | Uniquely identifies the alternate act identifier.                                                     |
| <p>IdentifierTypeId<br> [0..1]</p>           | UUID    | Identifies the type of identifier this particular identifier instance represents (order #, etc.)      |
| <p>AssigningAuthorityId<br> [1..1]</p>       | UUID    | Identifies the authority that assigned the identifier.                                                |
| <p>IdentifierValue<br> [1..1]</p>            | VARCHAR | The actual external identifier value.                                                                 |
| <p>EffectiveVersionSequenceId<br> [1..1]</p> | UUID    | Identifies the version of the act where the alternate identifier became active.                       |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>  | UUID    | When present, identifies the version of the act whereby the alternate identifier is no longer active. |

### ActExtension Entity

The act extension table is used to store extensions attached to acts.

| Column                                       | Type      | Description                                                                                                                                          |
| -------------------------------------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>ActExtensionId<br> [1..1]</p>             | UUID      | A unique identifier for the act extension.                                                                                                           |
| <p>ExtensionTypeId<br> [1..1]</p>            | UUID      | Identifies the type of extension represented. This includes information on how the extension should be serialized to/from the ExtensionValue column. |
| <p>ExtensionValue<br> [1..1]</p>             | VARBINARY | Carries the value of the extension.                                                                                                                  |
| <p>ExtensionDisplay<br> [1..1]</p>           | VARCHAR   | A human comprehendible display value for the extension.                                                                                              |
| <p>EffectiveVersionSequenceId<br> [1..1]</p> | UUID      | Indicates the version of the act where this extension became active.                                                                                 |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>  | UUID      | When present, indicates the version of the act where the extension is no longer active.                                                              |

### Observation Entity

The observation table is used to store extended values related to observation act types.

| Column                                                       | Type | Description                                                                   |
| ------------------------------------------------------------ | ---- | ----------------------------------------------------------------------------- |
| <p>ActVersionId<br> [1..1]</p>                               | UUID | Identifies the act version to which this extended data applies.               |
| <p>InterpretationConceptId<br> [0..1] ~ActInterpretation</p> | UUID | Identifies the concept that represents the interpretation of the observation. |

### QuantityObservation Entity

The quantity observation table is used to store extended information related to the observations that carry quantified values.

| Column                                                  | Type    | Description                                                                              |
| ------------------------------------------------------- | ------- | ---------------------------------------------------------------------------------------- |
| <p>ActVersionId<br> [1..1]</p>                          | UUID    | Identifies the observation act version to which the quantified observation data applies. |
| <p>Quantity<br> [1..1]</p>                              | DECIMAL | A decimal value that contains the value of the observation quantity.                     |
| <p>QuantityPrecision<br> [1..1]</p>                     | INT     | Identifies the precision of the Quantity field.                                          |
| <p>UnitOfMeasureConceptId<br> [1..1] ~UnitOfMeasure</p> | UUID    | Identifies the concept that identifies the units of measurement.                         |

### TextObservation Entity

The text observation table is used to store additional information related to a text valued observation.

| Column                         | Type | Description                                                                           |
| ------------------------------ | ---- | ------------------------------------------------------------------------------------- |
| <p>ActVersionId<br> [1..1]</p> | UUID | Identifies the observation version id that this text observation data is attached to. |
| <p>TextValue<br> [1..1]</p>    | TEXT | A textual field that contains the observation data.                                   |

### CodedObservation Entity

The coded observation table is used to store additional data related to observations that are coded. Problems and Allergies would qualify as coded observations.

| Column                           | Type | Description                                                                               |
| -------------------------------- | ---- | ----------------------------------------------------------------------------------------- |
| <p>ActVersionId<br> [1..1]</p>   | UUID | Identifies the version of the observation that this coded observation value data applies. |
| <p>ConceptValueId<br> [1..1]</p> | UUID | Identifies the concept that represents the value of observation.                          |

### SubstanceAdministration Entity

The substance administration table is used to store data related to substance administrations to a patient. This include vaccines or any type of Epupin injections for

| Column                                             | Type    | Description                                                                                                                                           |
| -------------------------------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>ActVersionId<br> [1..1]</p>                     | UUID    | Identifies the act version to which the substance administration data applies.                                                                        |
| <p>RouteConceptId<br> [0..1] ~RouteConcept</p>     | UUID    | Identifies the concept that describes the route that was taken to administer the substance. This may be drawn from the default route if not supplied. |
| <p>DoseQuantity<br> [1..1]</p>                     | DECIMAL | Identifies the dosage that was given to the patient.                                                                                                  |
| <p>DoseQuantityPrecision<br> [1..1]</p>            | INT     | Identifies the precision of the dose quantity.                                                                                                        |
| <p>DoseUnitConceptId<br> [1..1] ~UnitOfMeasure</p> | INT     | Identifies the dose unit of measure that was given to the patient.                                                                                    |
| <p>SequenceId<br> [0..1]</p>                       | INT     | Identifies the sequence of this dose if it is a part of a sequence of doses.                                                                          |

### PatientEncounter Entity

The patient encounter table is used to store additional data related to an act that represents a patient encounter.

| Column                                                                | Type | Description                                                              |
| --------------------------------------------------------------------- | ---- | ------------------------------------------------------------------------ |
| <p>ActVersionId<br> [1..1]</p>                                        | UUID | Identifies the act to which the extended patient encounter data applies. |
| <p>DischargeDispositionConceptId<br> [0..1] ~DischargeDisposition</p> | UUID | Identifies the disposition in which the patient left the encounter.      |

### ActNote Entity

The act note table is used to store notes associated with an act.

| Column                                       | Type | Description                                                                          |
| -------------------------------------------- | ---- | ------------------------------------------------------------------------------------ |
| <p>ActNoteId<br> [1..1]</p>                  | UUID | A unique identifier for the note.                                                    |
| <p>EffectiveVersionSequenceId<br> [1..1]</p> | UUID | The version whereby the note became effective                                        |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>  | UUID | When populated, indicates the version of the act where the note is no longer active. |
| <p>AuthorEntityId<br> [1..1]</p>             | UUID | The identifier of the entity that wrote the note.                                    |
| <p>NoteText<br> [1..1]</p>                   | TEXT | The textual content of the note.                                                     |

### Procedure Entity

Used to track acts which alter the physical state of an entity (i.e. surgeries, etc.)

| Column                                                     | Type | Description                                                                      |
| ---------------------------------------------------------- | ---- | -------------------------------------------------------------------------------- |
| <p>ActVersionId<br> [1..1]</p>                             | UUID | Points to the version of the Act which this procedure is describing.             |
| <p>MethodCodeId<br> [0..1] ~ProcedureTechniqueCode</p>     | UUID | Identifies the formal method for performing the procedure.                       |
| <p>ApproachSiteCodeId<br> [0..1] ~BodySiteOrSystemCode</p> | UUID | Identifies the manner in which the target site was approached for the procedure. |
| <p>TargetSiteCodeId<br> [0..1] ~BodySiteOrSystemCode</p>   | UUID | Identifies the body system/part which was the target of the procedure.           |

# Data Dictionary

The SanteDB entity model represents a series of tables which are responsible for the tracking of entities within the SanteDB data model. Entities represent people, places, organizations, things, etc. and are responsible for participating within acts in some capacity.

![](<../../../../.gitbook/assets/image (165).png>)

### Entity

The entity table is responsible for the storage of immutable attributes of an entity.

| Column                                                         | Type | Description                                                                                                                                                                                                              |
| -------------------------------------------------------------- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p>EntityId</p><p>[1..1]</p>                                   | UUID | Uniquely identifies the entity within the context of the SanteDB implementation.                                                                                                                                         |
| <p>TemplateDefinitionId<br> [0..1]</p>                         | UUID | Identifies the template which the entity instance implements.                                                                                                                                                            |
| <p>ClassConceptId<br> [1..1] ~EntityClassConcept</p>           | UUID | Identifies the concept that classifies the entity by a type. The classifier is used to determine “WHAT TYPE” of entity the tuple represents such as a person, material, manufactured material, organization, place, etc. |
| <p>DeterminerConceptId<br> [1..1] ~EntityDeterminerConcept</p> | UUID | Identifies the concept that classifies or determines the type of entity. This is either an INSTANCE or CLASS concept identifier.                                                                                         |

### Entity Tag

The entity tag table is used to store version independent tags associated with an entity. A tag does not result in new versions of the entity and is used to track additional data related to security and/or workflow related metadata.

| Column                                            | Type     | Description                                                                                                                      |
| ------------------------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------- |
| <p>EntityTagId<br> [1..1]</p>                     | UUID     | Uniquely identifies the entity tag.                                                                                              |
| <p>EntityId<br> [1..1]</p>                        | UUID     | Identifies the entity to which the tag is associated.                                                                            |
| <p>Key<br> [1..1]</p>                             | VARCHAR  | Qualifies the type of tag associated with the entity. That is to say, type of tag is represented in the tuple of the determiner. |
| <p>Value<br> [1..1]</p>                           | VARCHAR  | A value that carries the data associated with the tag value.                                                                     |
| <p>CreationTime<br> [1..1]</p>                    | DATETIME | Indicates the date/time at which time the tag was created.                                                                       |
| <p>CreatedBy<br> [1..1]</p>                       | UUID     | Identifies the user that was responsible for the creation of the tag.                                                            |
| <p>ObsoletionTime<br> [0..1] ?(>CreationTime)</p> | DATETIME | When populated, indicates the time when the tag is no longer associated with the entity.                                         |
| <p>ObsoletedBy<br> [0..1] ?(ObsoletionTime)</p>   | UUID     | Identifies the user that was responsible for obsoleting the tag.                                                                 |

### Entity Version

The entity version table is used to store the mutable attributes of an entity, that is to say, any fields associated with an entity that may evolve over the lifespan of the entity are tracked in this table.

| Column                                                 | Type     | Description                                                                                                                                              |
| ------------------------------------------------------ | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>EntityVersionId<br> [1..1]</p>                      | UUID     | Uniquely identifies the version of the entity represented in the tuple.                                                                                  |
| <p>EntityId<br> [1..1]</p>                             | UUID     | Identifies the entity to which this version applies.                                                                                                     |
| <p>ReplacesVersionId<br> [0..1]</p>                    | UUID     | Identifies the version of the entity that the current tuple is responsible for replacing.                                                                |
| <p>StatusConceptId<br> [1..1] ~EntityStatusConcept</p> | UUID     | Identifies the status of the entity as of the version represented in the tuple.                                                                          |
| <p>CreationTime<br> [1..1]</p>                         | DATETIME | Indicates the time when the entity was created.                                                                                                          |
| <p>CreatedBy<br> [1..1]</p>                            | UUID     | Identifies the user that was responsible for the creation of the entity.                                                                                 |
| <p>ObsoletionTime<br> [0..1] ?(>CreationTime)</p>      | DATETIME | When populated, indicates the time when the entity version became obsolete.                                                                              |
| <p>ObsoletedBy<br> [0..1] ?(ObsoletionTime)</p>        | UUID     | Identifies the user that was responsible for the obsoleting of the record.                                                                               |
| <p>TypeConceptId<br> [0..1]</p>                        | UUID     | Indicates the concept that classifies the subtype of entity. For example, an entity may be a provider; however, the sub-type may be a “physiotherapist”. |

### Entity Relationship

The entity association table is used to associate two or more entities together. An association is made between a source entity and a target entity.

| Column                                                              | Type | Description                                                                                                                                                              |
| ------------------------------------------------------------------- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p>EntityRelationshipId<br> [1..1]</p>                              | UUID | Uniquely identifies the entity association.                                                                                                                              |
| <p>SourceEntityId<br> [1..1]</p>                                    | UUID | Identifies the source of the entity association.                                                                                                                         |
| <p>TargetEntityId<br> [1..1]</p>                                    | UUID | Identifies the target of the entity association.                                                                                                                         |
| <p>EffectiveVersionSequenceId<br> [1..1]</p>                        | UUID | Indicates the version of the source entity at which time this entity association was created or became effective.                                                        |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>                         | UUID | When populated, indicates that the entity association is no longer active, and indicates the version of the source entity where the association ceased to be applicable. |
| <p>RelationshipTypeConceptId<br> [1..1] ~EntityRelationshipType</p> | UUID | Classifies the relationship between the two entities. Can indicate ownership roles such as “Place OWNS Material”, or relationship “Patient CHILD OF Person”.             |
| <p>Quantity<br> [1..1] = 1</p>                                      | INT  | Indicates the quantity of target entities contained within the source entity.                                                                                            |

### Entity Note

The entity note table is used to store textual notes related to an entity.

| Column                                       | Type | Description                                                                               |
| -------------------------------------------- | ---- | ----------------------------------------------------------------------------------------- |
| <p>EntityNoteId<br> [1..1]</p>               | UUID | Uniquely identifies the note.                                                             |
| <p>EffectiveVersionSequenceId<br> [1..1]</p> | UUID | Identifies the version of the entity to which the note applies.                           |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>  | UUID | When populated, indicates the version of the entity where the note is no longer relevant. |
| <p>AuthorEntityId<br> [1..1]</p>             | UUID | Identifies the entity that was responsible for the authoring of the note.                 |
| <p>NoteText<br> [1..1]</p>                   | TEXT | Indicates the textual content of the note.                                                |

### Entity Address

The entity address table is used to store address information (physical addresses) related to an entity.

| Column                                                | Type | Description                                                                                                      |
| ----------------------------------------------------- | ---- | ---------------------------------------------------------------------------------------------------------------- |
| <p>EntityAddressId<br> [1..1]</p>                     | UUID | Uniquely identifies the entity address.                                                                          |
| <p>EffectiveVersionSequenceId<br> [1..1]</p>          | UUID | Identifies the version of the entity whereby the address information became active.                              |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>           | UUID | When populated, indicates the version of the entity whereby the address is no longer applicable.                 |
| <p>AddressUseConceptId<br> [1..1] ~AddressUseType</p> | UUID | Indicates the desired use of the address. Examples include physical visit, vacation home, contact, mailing, etc. |

### Entity Address Component

The entity address component table is used to store the address components associated with a particular entity address.

| Column                                                      | Type    | Description                                                                                                                         |
| ----------------------------------------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| <p>EntityAddressComponentId<br> [1..1]</p>                  | UUID    | Uniquely identifies the entity address component.                                                                                   |
| <p>Value<br> [1..1]</p>                                     | VARCHAR | Identifies the value of the of the address component                                                                                |
| <p>ComponentTypeConceptId<br> [1..1] ~NameComponentType</p> | UUID    | Classifies the type of address component represented in the value field. For example: street name, city, country, postal code, etc. |
| <p>EntityAddressId<br> [1..1]</p>                           | UUID    | Identifies the entity address to which the entity address component applies.                                                        |

### Entity Name

The entity name table is used to store master list of names associated with an entity.

| Column                                       | Type | Description                                                                                                        |
| -------------------------------------------- | ---- | ------------------------------------------------------------------------------------------------------------------ |
| <p>EntityNameId<br> [1..1]</p>               | UUID | Uniquely identifies the entity name.                                                                               |
| <p>EntityNameUseId<br> [1..1]</p>            | UUID | Classified the intended use of the entity name. Examples: maiden name, legal name, license name, artist name, etc. |
| <p>EffectiveVersionSequenceId<br> [1..1]</p> | UUID | Identifies the version of the entity when this name became active.                                                 |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>  | UUID | When populated, identifies the version of the entity where the name is no longer active.                           |

### Entity Name Component

The entity name component table is responsible for the storage of name components that comprise an entity name.

| Column                                                            | Type | Description                                                                                       |
| ----------------------------------------------------------------- | ---- | ------------------------------------------------------------------------------------------------- |
| <p>NameComponentId<br> [1..1]</p>                                 | UUID | Uniquely identifies the name component.                                                           |
| <p>ValueId<br> [1..1]</p>                                         | UUID | Indicates the phonetic value tuple that stores the name value.                                    |
| <p>NameComponentTypeConceptId<br> [1..1] ~EntityComponentType</p> | UUID | Classifies the type of name component represented. Examples: first name, title, family name, etc. |
| <p>EntityNameId<br> [1..1]</p>                                    | UUID | Indicates the entity name to which the name component applies.                                    |

### Entity Identifier

The entity identifier is table is responsible for the storage of alternate identifies associated with the entity.

| Column                                       | Type    | Description                                                                                                                                  |
| -------------------------------------------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>EntityIdentifierId<br> [1..1]</p>         | UUID    | Uniquely identifies the entity identifier.                                                                                                   |
| <p>IdentifierTypeId<br> [1..1]</p>           | UUID    | Classifies the type of identifier that is represented by the entity identifier. Examples: business identifier, mrn, primary identifier, etc. |
| <p>EffectiveVersionSequenceId<br> [1..1]</p> | UUID    | Indicates the version of the entity when the identifier became active.                                                                       |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>  | UUID    | When populated, indicates the version of the entity where the identifier is no longer active.                                                |
| <p>AssigningAuthorityId<br> [1..1]</p>       | UUID    | Identifies the authority that was responsible for the assigning of the identifier.                                                           |
| <p>IdentifierValue<br> [1..1]</p>            | VARCHAR | Indicates the value of the entity identifier.                                                                                                |

### Entity Extension

The entity extension table is used to store additional, clinically relevant, versioned data attached to an entity that cannot be stored in the native data model.

| Column                                       | Type      | Description                                                                                                 |
| -------------------------------------------- | --------- | ----------------------------------------------------------------------------------------------------------- |
| <p>EntityExtensionId<br> [1..1]</p>          | UUID      | Uniquely identifies the extension.                                                                          |
| <p>EffectiveVersionSequenceId<br> [1..1]</p> | UUID      | Indicates the version of the entity when the extension data did become active.                              |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>  | UUID      | When populated, indicates the version of the entity where the extension value is no longer applicable.      |
| <p>ExtensionTypeId<br> [1..1]</p>            | UUID      | Indicates the type, or handler, for the extension data.                                                     |
| <p>ExtensionData<br> [1..1]</p>              | VARBINARY | Serialized data that contains the raw value of the extension (serialized and de-serialized by the handler). |
| <p>ExtensionDisplay<br> [1..1]</p>           | VARCHAR   | A textual, human readable expression of the extension value which can be displayed on reports, etc.         |

### Entity Telecom Address

The entity telecommunications address table is used to store data related to telecommunications addresses (email, fax, phone, etc.) for an entity.

| Column                                                   | Type    | Description                                                                                        |
| -------------------------------------------------------- | ------- | -------------------------------------------------------------------------------------------------- |
| <p>EntityTelecomId<br> [1..1]</p>                        | UUID    | Uniquely identifies the telecommunications address.                                                |
| <p>TelecomAddressType<br> [1..1] ~TelecomAddressType</p> | UUID    | Classifies the type of address represented (example: phone, fax, email, etc.)                      |
| <p>TelecomAddress<br> [1..1]</p>                         | VARCHAR | The value of the telecommunications address in RFC-2396 format.                                    |
| <p>TelecomUseConceptId<br> [0..1] ~TelecomAddressUse</p> | UUID    | Identifies the intended use of the telecom address. (Example: home, work, etc.)                    |
| <p>EffectiveVersionSequenceId<br> [1..1]</p>             | UUID    | Identifies the version of the entity whereby the telecom address became effective.                 |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>              | UUID    | When populated, identifies the version of the entity where the telecom address is no longer valid. |

### Place

The place table represents a specialization of the Entity table which is used to represent physical places such as clinics, outreach activity sites, etc.

| Column                              | Type  | Description                                                            |
| ----------------------------------- | ----- | ---------------------------------------------------------------------- |
| <p>EntityVersionId<br> [1..1]</p>   | UUID  | Identifies the version of the entity to which the place data applies.  |
| <p>MobileInd<br> [1..1] = False</p> | BIT   | Indicator that is used to identify that a place is mobile.             |
| <p>Lat<br> [0..1]</p>               | FLOAT | The latitudinal position of the place expressed in degrees latitude.   |
| <p>Lng<br> [0..1]</p>               | FLOAT | The longitudinal position of the place expressed in degrees longitude. |

### Place Service

The place service table is used to identify the services that are provided at a particular place. Services may include stocking, transfer depots, immunization.

| Column                                          | Type    | Description                                                                                           |
| ----------------------------------------------- | ------- | ----------------------------------------------------------------------------------------------------- |
| <p>PlaceServiceId<br> [1..1]</p>                | UUID    | A unique identifier for the place service.                                                            |
| <p>EffectiveVersionSequenceId<br> [1..1]</p>    | UUID    | The version of the place entity where the service entry is active.                                    |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>     | UUID    | When populated, indicates the version of the place entity where the service entry is no longer valid. |
| <p>ServiceConceptId<br> [1..1] ~ServiceType</p> | UUID    | Indicates a concept that describes the service offered.                                               |
| <p>ServiceSchedule<br> [0..1]</p>               | XML     | An XML expression of the service schedule.                                                            |
| <p>ServiceScheduleType<br> [0..1]</p>           | VARCHAR | Identifies the type of data stored in the service schedule column (iCal, GTS, etc.)                   |

### Application Entity

The application entity table is used to store entity data related to an application. An application is a software program that runs on a device. This differs from a security application, in that an application may be referenced clinically without needing access to the SanteDB system. For example: The patient uses MyPHR

| Column                            | Type    | Description                                                                             |
| --------------------------------- | ------- | --------------------------------------------------------------------------------------- |
| <p>EntityVersionId<br> [1..1]</p> | UUID    | Identifies the version of the entity to which the application data applies.             |
| <p>SoftwareName<br> [0..1]</p>    | VARCHAR | Identifies the name of the software package (“EMR Package” is an example)               |
| <p>VersionName<br> [0..1]</p>     | VARCHAR | Identifies the version of the software (example: “1.0”)                                 |
| <p>VendorName<br> [0..1]</p>      | VARCHAR | The name of the vendor which distributes the software application (example: “ABC Corp”) |
| <p>ApplicationId<br> [0..1]</p>   | UUID    | When populated, links the application entity to a security application.                 |

### Device Entity

The device table is used to store clinical information related to a physical device. Like an application entity, this table is used to describe the clinical attributes of a device used in the provisioning of care. Example: Bob’s Insulin Pump. The insulin pump itself may have no security device as it doesn’t require access to SanteDB.

| Column                                | Type    | Description                                                                       |
| ------------------------------------- | ------- | --------------------------------------------------------------------------------- |
| <p>EntityVersionId<br> [1..1]</p>     | UUID    | Indicates the version of the entity to which the device data applies.             |
| <p>ManufacturerModel<br> [0..1]</p>   | VARCHAR | Indicates the name of the manufacturer of the device.                             |
| <p>OperatingSystemName<br> [0..1]</p> | VARCHAR | Indicates the name of the operating system installed on the device.               |
| <p>DeviceId<br> [0..1]</p>            | UUID    | When populated, identifies the security device associated with the device entity. |

### Material

A material represents a physical thing (syringe, drug, etc.) which participates in an act or is assigned to a person.

| Column                                             | Type     | Description                                                                                                                                                                                |
| -------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p>EntityVersionId<br> [1..1]</p>                  | UUID     | Identifies the version of the entity to which the material data applies.                                                                                                                   |
| <p>ExpiryTime<br> [1..1]</p>                       | DATETIME | Indicates the time when the material will expire.                                                                                                                                          |
| <p>ExpiryTimePrecision<br> [1..1]</p>              | CHAR     | Indicates the precision that the expiry time has.                                                                                                                                          |
| <p>FormConceptId<br> [0..1] ~MaterialForm</p>      | UUID     | Identifies a concept that denotes the form that the material takes. Examples: capsule, injection, nebulizer, etc. For drugs and vaccines, the form will imply the route of administration. |
| <p>QuantityConceptId<br> [0..1] ~UnitOfMeasure</p> | UUID     | Indicates the unit of measure for a single unit of the material. Examples: dose, mL, etc.                                                                                                  |
| <p>Quantity<br> [0..1] = 1</p>                     | NUMERIC  | Indicates the reference quantity in UOM. For example, BCG MMAT is 5 mL of BCG Antigen                                                                                                      |
| <p>IsAdministrative<br> [1..1] = false</p>         | BIT      | An indicator that is used to identify whether the material is a real material or an administrative material for the purpose of management.                                                 |

### Manufactured Material

A manufactured material is a specialization of a material that is manufactured.&#x20;

| Column                            | Type    | Description                                                                  |
| --------------------------------- | ------- | ---------------------------------------------------------------------------- |
| <p>EntityVersionId<br> [1..1]</p> | UUID    | Indicates the version of the material to which the specialized data applies. |
| <p>LotNumber<br> [1..1]</p>       | VARCHAR | Indicates the manufacturer lot for the material.                             |

### Person

A person is a specialization of Entity that is used to represent a human.

| Column                                 | Type | Description                                                 |
| -------------------------------------- | ---- | ----------------------------------------------------------- |
| <p>EntityVersionId<br> [1..1]</p>      | N/A  | The version of the entity to which the person data applies. |
| <p>DateOfBirth<br> [0..1]</p>          | DATE | Indicates the date on which the person entity was born.     |
| <p>DateOfBirthPrecision<br> [0..1]</p> | CHAR | Indicates the precision of the date of birth field.         |

### Person Communication Language

The person language communication table is used to store information related to the person’s language preferences. This can be used by the user interface to determine which language to display, however is also clinically relevant to indicate the language in which a patient wishes to receive communciations.

| Column                                              | Type    | Description                                                                                                          |
| --------------------------------------------------- | ------- | -------------------------------------------------------------------------------------------------------------------- |
| <p>PersonLanaugeCommunication<br> Id<br> [1..1]</p> | UUID    | Uniquely identifies the language of communication.                                                                   |
| <p>EffectiveVersionSequenceId<br> [1..1]</p>        | UUID    | Indicates the version of the person entity whereby the language of communication is effective.                       |
| <p>ObsoleteVersionSequenceId<br> [0..1]</p>         | UUID    | When present, indicates the version of the person entity where the language of communication is no longer effective. |
| <p>LanguageCommunication<br> [1..1] ~ISO639-2</p>   | VARCHAR | An ISO-639-2 language code indicating the language preference.                                                       |
| <p>PreferenceIndicator<br> [0..1] = False</p>       | BIT     | Indicates whether the person prefers the language for communications.                                                |

### Organization

The organization table represents a specialization of an entity representing a logical organization.

| Column                                               | Type | Description                                                                                      |
| ---------------------------------------------------- | ---- | ------------------------------------------------------------------------------------------------ |
| <p>EntityVersionId<br> [1..1]</p>                    | UUID | Indicates the version of the entity to which the organization specialization applies.            |
| <p>IndustryConceptId<br> [0..1] ~IndustryConcept</p> | UUID | Indicates the industry in which the organization operates. Examples: logistics, healthcare, etc. |

### Provider

A provider is a specialization of the Person table which is used to store provider related information about a person.

| Column                                 | Type | Description                                                                       |
| -------------------------------------- | ---- | --------------------------------------------------------------------------------- |
| <p>EntityVersionId<br> [1..1]</p>      | UUID | Indicates the version of the entity to which the provider specialization applies. |
| <p>SpecialtyConceptId</p><p>[1..1]</p> | UUID | Indicates the primary specialty of the provider at this version of the record.    |

### Patient

The patient entity is a specialization of the Person table which is used to track primary attributes related to a patient.

| Column                                                            | Type     | Description                                                                                                                                                                                                                   |
| ----------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>EntityVersionId<br> [1..1]</p>                                 | UUID     | Indicates the version of the entity to which the patient specialization applies.                                                                                                                                              |
| <p>GenderConceptId</p><p>[1..1] ~AdministrativeGender</p>         | UUID     | Identifies the logical gender concept of the patient. These values are drawn from the administrative gender concept set.                                                                                                      |
| <p>DeceasedTime</p><p>[0..1]</p>                                  | DATETIME | When populated, indicates the date/time that the patient was indicated as deceased.                                                                                                                                           |
| <p>DeceasedTimePrecision</p><p>[0..1]</p>                         | INT      | When populated, controls the precision of the value in DeceasedTime                                                                                                                                                           |
| <p>MultipleBirthOrder</p><p>[0..1]</p>                            | INT      | When populated, indicates the order of the patient in a multiple birth. A non-null value in this column (0 or -1) indicates special indicators that the exact order is unknown, however the patient is part of a multi-birth. |
| <p>MaritalStatusConceptId</p><p>[0..1] ~MaritalStatus</p>         | UUID     | The codified status of the patient's marital state (example: single, married, divorced, etc.). Drawn from the MaritalStatus concept set.                                                                                      |
| <p>EducationLevelConceptId</p><p>[0..1] ~EducationLevel</p>       | UUID     | The codified value indicating the patient's highest level of education obtained (college, high school, etc.)                                                                                                                  |
| <p>LivingArrangementConceptId</p><p>[0..1] ~LivingArrangement</p> | UUID     | The codified value indicating the patient's living arrangement (cohabitating, supervised care, etc.)                                                                                                                          |
| <p>ReligionConceptId</p><p>[0..1] ~Religion</p>                   | UUID     | The codified value indicating the patient's religion. Note that the religion concept may be blocked based on national profiles and local legislation.                                                                         |
| <p>EthnicGroupConceptId</p><p>[0..1] ~EthnicGroup</p>             | UUID     | The codified value indicating the patient's ethnicity.                                                                                                                                                                        |

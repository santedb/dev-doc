# Data Dictionary

The SanteDB entity model represents a series of tables which are responsible for the tracking of entities within the SanteDB data model. Entities represent people, places, organizations, things, etc. and are responsible for participating within acts in some capacity.

![](../../../../../.gitbook/assets/image%20%28150%29.png)

### Entity

The entity table is responsible for the storage of immutable attributes of an entity.

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
      <td style="text-align:left">
        <p>EntityId</p>
        <p>[1..1]</p>
      </td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Uniquely identifies the entity within the context of the SanteDB implementation.</td>
    </tr>
    <tr>
      <td style="text-align:left">TemplateDefinitionId
        <br />[0..1]</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Identifies the template which the entity instance implements.</td>
    </tr>
    <tr>
      <td style="text-align:left">ClassConceptId
        <br />[1..1] ~EntityClassConcept</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Identifies the concept that classifies the entity by a type. The classifier
        is used to determine &#x201C;WHAT TYPE&#x201D; of entity the tuple represents
        such as a person, material, manufactured material, organization, place,
        etc.</td>
    </tr>
    <tr>
      <td style="text-align:left">DeterminerConceptId
        <br />[1..1] ~EntityDeterminerConcept</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Identifies the concept that classifies or determines the type of entity.
        This is either an INSTANCE or CLASS concept identifier.</td>
    </tr>
  </tbody>
</table>

### Entity Tag

The entity tag table is used to store version independent tags associated with an entity. A tag does not result in new versions of the entity and is used to track additional data related to security and/or workflow related metadata.

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityTagId  \[1..1\] | UUID | Uniquely identifies the entity tag. |
| EntityId  \[1..1\] | UUID | Identifies the entity to which the tag is associated. |
| Key  \[1..1\] | VARCHAR | Qualifies the type of tag associated with the entity. That is to say, type of tag is represented in the tuple of the determiner. |
| Value  \[1..1\] | VARCHAR | A value that carries the data associated with the tag value. |
| CreationTime  \[1..1\] | DATETIME | Indicates the date/time at which time the tag was created. |
| CreatedBy  \[1..1\] | UUID | Identifies the user that was responsible for the creation of the tag. |
| ObsoletionTime  \[0..1\] ?\(&gt;CreationTime\) | DATETIME | When populated, indicates the time when the tag is no longer associated with the entity. |
| ObsoletedBy  \[0..1\] ?\(ObsoletionTime\) | UUID | Identifies the user that was responsible for obsoleting the tag. |

### Entity Version

The entity version table is used to store the mutable attributes of an entity, that is to say, any fields associated with an entity that may evolve over the lifespan of the entity are tracked in this table.

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityVersionId  \[1..1\] | UUID | Uniquely identifies the version of the entity represented in the tuple. |
| EntityId  \[1..1\] | UUID | Identifies the entity to which this version applies. |
| ReplacesVersionId  \[0..1\] | UUID | Identifies the version of the entity that the current tuple is responsible for replacing. |
| StatusConceptId  \[1..1\] ~EntityStatusConcept | UUID | Identifies the status of the entity as of the version represented in the tuple. |
| CreationTime  \[1..1\] | DATETIME | Indicates the time when the entity was created. |
| CreatedBy  \[1..1\] | UUID | Identifies the user that was responsible for the creation of the entity. |
| ObsoletionTime  \[0..1\] ?\(&gt;CreationTime\) | DATETIME | When populated, indicates the time when the entity version became obsolete. |
| ObsoletedBy  \[0..1\] ?\(ObsoletionTime\) | UUID | Identifies the user that was responsible for the obsoleting of the record. |
| TypeConceptId  \[0..1\] | UUID | Indicates the concept that classifies the subtype of entity. For example, an entity may be a provider; however, the sub-type may be a “physiotherapist”. |

### Entity Relationship

The entity association table is used to associate two or more entities together. An association is made between a source entity and a target entity.

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityRelationshipId  \[1..1\] | UUID | Uniquely identifies the entity association. |
| SourceEntityId  \[1..1\] | UUID | Identifies the source of the entity association. |
| TargetEntityId  \[1..1\] | UUID | Identifies the target of the entity association. |
| EffectiveVersionSequenceId  \[1..1\] | UUID | Indicates the version of the source entity at which time this entity association was created or became effective. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | When populated, indicates that the entity association is no longer active, and indicates the version of the source entity where the association ceased to be applicable. |
| RelationshipTypeConceptId  \[1..1\] ~EntityRelationshipType | UUID | Classifies the relationship between the two entities. Can indicate ownership roles such as “Place OWNS Material”, or relationship “Patient CHILD OF Person”. |
| Quantity  \[1..1\] = 1 | INT | Indicates the quantity of target entities contained within the source entity. |

### Entity Note

The entity note table is used to store textual notes related to an entity.

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityNoteId  \[1..1\] | UUID | Uniquely identifies the note. |
| EffectiveVersionSequenceId  \[1..1\] | UUID | Identifies the version of the entity to which the note applies. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | When populated, indicates the version of the entity where the note is no longer relevant. |
| AuthorEntityId  \[1..1\] | UUID | Identifies the entity that was responsible for the authoring of the note. |
| NoteText  \[1..1\] | TEXT | Indicates the textual content of the note. |

### Entity Address

The entity address table is used to store address information \(physical addresses\) related to an entity.

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityAddressId  \[1..1\] | UUID | Uniquely identifies the entity address. |
| EffectiveVersionSequenceId  \[1..1\] | UUID | Identifies the version of the entity whereby the address information became active. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | When populated, indicates the version of the entity whereby the address is no longer applicable. |
| AddressUseConceptId  \[1..1\] ~AddressUseType | UUID | Indicates the desired use of the address. Examples include physical visit, vacation home, contact, mailing, etc. |

### Entity Address Component

The entity address component table is used to store the address components associated with a particular entity address.

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityAddressComponentId  \[1..1\] | UUID | Uniquely identifies the entity address component. |
| Value  \[1..1\] | VARCHAR | Identifies the value of the of the address component |
| ComponentTypeConceptId  \[1..1\] ~NameComponentType | UUID | Classifies the type of address component represented in the value field. For example: street name, city, country, postal code, etc. |
| EntityAddressId  \[1..1\] | UUID | Identifies the entity address to which the entity address component applies. |

### Entity Name

The entity name table is used to store master list of names associated with an entity.

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityNameId  \[1..1\] | UUID | Uniquely identifies the entity name. |
| EntityNameUseId  \[1..1\] | UUID | Classified the intended use of the entity name. Examples: maiden name, legal name, license name, artist name, etc. |
| EffectiveVersionSequenceId  \[1..1\] | UUID | Identifies the version of the entity when this name became active. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | When populated, identifies the version of the entity where the name is no longer active. |

### Entity Name Component

The entity name component table is responsible for the storage of name components that comprise an entity name.

| Column | Type | Description |
| :--- | :--- | :--- |
| NameComponentId  \[1..1\] | UUID | Uniquely identifies the name component. |
| ValueId  \[1..1\] | UUID | Indicates the phonetic value tuple that stores the name value. |
| NameComponentTypeConceptId  \[1..1\] ~EntityComponentType | UUID | Classifies the type of name component represented. Examples: first name, title, family name, etc. |
| EntityNameId  \[1..1\] | UUID | Indicates the entity name to which the name component applies. |

### Entity Identifier

The entity identifier is table is responsible for the storage of alternate identifies associated with the entity.

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityIdentifierId  \[1..1\] | UUID | Uniquely identifies the entity identifier. |
| IdentifierTypeId  \[1..1\] | UUID | Classifies the type of identifier that is represented by the entity identifier. Examples: business identifier, mrn, primary identifier, etc. |
| EffectiveVersionSequenceId  \[1..1\] | UUID | Indicates the version of the entity when the identifier became active. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | When populated, indicates the version of the entity where the identifier is no longer active. |
| AssigningAuthorityId  \[1..1\] | UUID | Identifies the authority that was responsible for the assigning of the identifier. |
| IdentifierValue  \[1..1\] | VARCHAR | Indicates the value of the entity identifier. |

### Entity Extension

The entity extension table is used to store additional, clinically relevant, versioned data attached to an entity that cannot be stored in the native data model.

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityExtensionId  \[1..1\] | UUID | Uniquely identifies the extension. |
| EffectiveVersionSequenceId  \[1..1\] | UUID | Indicates the version of the entity when the extension data did become active. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | When populated, indicates the version of the entity where the extension value is no longer applicable. |
| ExtensionTypeId  \[1..1\] | UUID | Indicates the type, or handler, for the extension data. |
| ExtensionData  \[1..1\] | VARBINARY | Serialized data that contains the raw value of the extension \(serialized and de-serialized by the handler\). |
| ExtensionDisplay  \[1..1\] | VARCHAR | A textual, human readable expression of the extension value which can be displayed on reports, etc. |

### Entity Telecom Address

The entity telecommunications address table is used to store data related to telecommunications addresses \(email, fax, phone, etc.\) for an entity.

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityTelecomId  \[1..1\] | UUID | Uniquely identifies the telecommunications address. |
| TelecomAddressType  \[1..1\] ~TelecomAddressType | UUID | Classifies the type of address represented \(example: phone, fax, email, etc.\) |
| TelecomAddress  \[1..1\] | VARCHAR | The value of the telecommunications address in RFC-2396 format. |
| TelecomUseConceptId  \[0..1\] ~TelecomAddressUse | UUID | Identifies the intended use of the telecom address. \(Example: home, work, etc.\) |
| EffectiveVersionSequenceId  \[1..1\] | UUID | Identifies the version of the entity whereby the telecom address became effective. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | When populated, identifies the version of the entity where the telecom address is no longer valid. |

### Place

The place table represents a specialization of the Entity table which is used to represent physical places such as clinics, outreach activity sites, etc.

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityVersionId  \[1..1\] | UUID | Identifies the version of the entity to which the place data applies. |
| MobileInd  \[1..1\] = False | BIT | Indicator that is used to identify that a place is mobile. |
| Lat  \[0..1\] | FLOAT | The latitudinal position of the place expressed in degrees latitude. |
| Lng  \[0..1\] | FLOAT | The longitudinal position of the place expressed in degrees longitude. |

### Place Service

The place service table is used to identify the services that are provided at a particular place. Services may include stocking, transfer depots, immunization.

| Column | Type | Description |
| :--- | :--- | :--- |
| PlaceServiceId  \[1..1\] | UUID | A unique identifier for the place service. |
| EffectiveVersionSequenceId  \[1..1\] | UUID | The version of the place entity where the service entry is active. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | When populated, indicates the version of the place entity where the service entry is no longer valid. |
| ServiceConceptId  \[1..1\] ~ServiceType | UUID | Indicates a concept that describes the service offered. |
| ServiceSchedule  \[0..1\] | XML | An XML expression of the service schedule. |
| ServiceScheduleType  \[0..1\] | VARCHAR | Identifies the type of data stored in the service schedule column \(iCal, GTS, etc.\) |

### Application Entity

The application entity table is used to store entity data related to an application. An application is a software program that runs on a device. This differs from a security application, in that an application may be referenced clinically without needing access to the SanteDB system. For example: The patient uses MyPHR

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityVersionId  \[1..1\] | UUID | Identifies the version of the entity to which the application data applies. |
| SoftwareName  \[0..1\] | VARCHAR | Identifies the name of the software package \(“EMR Package” is an example\) |
| VersionName  \[0..1\] | VARCHAR | Identifies the version of the software \(example: “1.0”\) |
| VendorName  \[0..1\] | VARCHAR | The name of the vendor which distributes the software application \(example: “ABC Corp”\) |
| ApplicationId  \[0..1\] | UUID | When populated, links the application entity to a security application. |

### Device Entity

The device table is used to store clinical information related to a physical device. Like an application entity, this table is used to describe the clinical attributes of a device used in the provisioning of care. Example: Bob’s Insulin Pump. The insulin pump itself may have no security device as it doesn’t require access to SanteDB.

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityVersionId  \[1..1\] | UUID | Indicates the version of the entity to which the device data applies. |
| ManufacturerModel  \[0..1\] | VARCHAR | Indicates the name of the manufacturer of the device. |
| OperatingSystemName  \[0..1\] | VARCHAR | Indicates the name of the operating system installed on the device. |
| DeviceId  \[0..1\] | UUID | When populated, identifies the security device associated with the device entity. |

### Material

A material represents a physical thing \(syringe, drug, etc.\) which participates in an act or is assigned to a person.

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityVersionId  \[1..1\] | UUID | Identifies the version of the entity to which the material data applies. |
| ExpiryTime  \[1..1\] | DATETIME | Indicates the time when the material will expire. |
| ExpiryTimePrecision  \[1..1\] | CHAR | Indicates the precision that the expiry time has. |
| FormConceptId  \[0..1\] ~MaterialForm | UUID | Identifies a concept that denotes the form that the material takes. Examples: capsule, injection, nebulizer, etc. For drugs and vaccines, the form will imply the route of administration. |
| QuantityConceptId  \[0..1\] ~UnitOfMeasure | UUID | Indicates the unit of measure for a single unit of the material. Examples: dose, mL, etc. |
| Quantity  \[0..1\] = 1 | NUMERIC | Indicates the reference quantity in UOM. For example, BCG MMAT is 5 mL of BCG Antigen |
| IsAdministrative  \[1..1\] = false | BIT | An indicator that is used to identify whether the material is a real material or an administrative material for the purpose of management. |

### Manufactured Material

A manufactured material is a specialization of a material that is manufactured. 

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityVersionId  \[1..1\] | UUID | Indicates the version of the material to which the specialized data applies. |
| LotNumber  \[1..1\] | VARCHAR | Indicates the manufacturer lot for the material. |

### Person

A person is a specialization of Entity that is used to represent a human.

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityVersionId  \[1..1\] | N/A | The version of the entity to which the person data applies. |
| DateOfBirth  \[0..1\] | DATE | Indicates the date on which the person entity was born. |
| DateOfBirthPrecision  \[0..1\] | CHAR | Indicates the precision of the date of birth field. |

### Person Communication Language

The person language communication table is used to store information related to the person’s language preferences. This can be used by the user interface to determine which language to display, however is also clinically relevant to indicate the language in which a patient wishes to receive communciations.

| Column | Type | Description |
| :--- | :--- | :--- |
| PersonLanaugeCommunication  Id  \[1..1\] | UUID | Uniquely identifies the language of communication. |
| EffectiveVersionSequenceId  \[1..1\] | UUID | Indicates the version of the person entity whereby the language of communication is effective. |
| ObsoleteVersionSequenceId  \[0..1\] | UUID | When present, indicates the version of the person entity where the language of communication is no longer effective. |
| LanguageCommunication  \[1..1\] ~ISO639-2 | VARCHAR | An ISO-639-2 language code indicating the language preference. |
| PreferenceIndicator  \[0..1\] = False | BIT | Indicates whether the person prefers the language for communications. |

### Organization

The organization table represents a specialization of an entity representing a logical organization.

| Column | Type | Description |
| :--- | :--- | :--- |
| EntityVersionId  \[1..1\] | UUID | Indicates the version of the entity to which the organization specialization applies. |
| IndustryConceptId  \[0..1\] ~IndustryConcept | UUID | Indicates the industry in which the organization operates. Examples: logistics, healthcare, etc. |

### Provider

A provider is a specialization of the Person table which is used to store provider related information about a person.

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
      <td style="text-align:left">EntityVersionId
        <br />[1..1]</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Indicates the version of the entity to which the provider specialization
        applies.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>SpecialtyConceptId</p>
        <p>[1..1]</p>
      </td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Indicates the primary specialty of the provider at this version of the
        record.</td>
    </tr>
  </tbody>
</table>

### Patient

The patient entity is a specialization of the Person table which is used to track primary attributes related to a patient.

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
      <td style="text-align:left">EntityVersionId
        <br />[1..1]</td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Indicates the version of the entity to which the patient specialization
        applies.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>GenderConceptId</p>
        <p>[1..1] ~AdministrativeGender</p>
      </td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">Identifies the logical gender concept of the patient. These values are
        drawn from the administrative gender concept set.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>DeceasedTime</p>
        <p>[0..1]</p>
      </td>
      <td style="text-align:left">DATETIME</td>
      <td style="text-align:left">When populated, indicates the date/time that the patient was indicated
        as deceased.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>DeceasedTimePrecision</p>
        <p>[0..1]</p>
      </td>
      <td style="text-align:left">INT</td>
      <td style="text-align:left">When populated, controls the precision of the value in DeceasedTime</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>MultipleBirthOrder</p>
        <p>[0..1]</p>
      </td>
      <td style="text-align:left">INT</td>
      <td style="text-align:left">When populated, indicates the order of the patient in a multiple birth.
        A non-null value in this column (0 or -1) indicates special indicators
        that the exact order is unknown, however the patient is part of a multi-birth.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>MaritalStatusConceptId</p>
        <p>[0..1] ~MaritalStatus</p>
      </td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">The codified status of the patient&apos;s marital state (example: single,
        married, divorced, etc.). Drawn from the MaritalStatus concept set.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>EducationLevelConceptId</p>
        <p>[0..1] ~EducationLevel</p>
      </td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">The codified value indicating the patient&apos;s highest level of education
        obtained (college, high school, etc.)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>LivingArrangementConceptId</p>
        <p>[0..1] ~LivingArrangement</p>
      </td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">The codified value indicating the patient&apos;s living arrangement (cohabitating,
        supervised care, etc.)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>ReligionConceptId</p>
        <p>[0..1] ~Religion</p>
      </td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">The codified value indicating the patient&apos;s religion. Note that the
        religion concept may be blocked based on national profiles and local legislation.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>EthnicGroupConceptId</p>
        <p>[0..1] ~EthnicGroup</p>
      </td>
      <td style="text-align:left">UUID</td>
      <td style="text-align:left">The codified value indicating the patient&apos;s ethnicity.</td>
    </tr>
  </tbody>
</table>


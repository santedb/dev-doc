`IDataPersistenceServiceEx&lt;TModel>` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Generic interface implementation

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|DeleteAll|void|*Expression&lt;Func&lt;TModel,Boolean>>* **matching**<br/>*TransactionMode* **mode**<br/>*IPrincipal* **principal**|Obsolete all matching data|
|Touch|TModel|*Guid* **key**<br/>*TransactionMode* **mode**<br/>*IPrincipal* **principal**|Touch the specified data|

# Implementations


## BaseEntityDataPersistenceService&lt;TModel,TDbModel> - (SanteDB.Persistence.Data)
Represents a persistence service which has behaviors to properly persist [BaseEntityData](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_BaseEntityData.htm)
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## BasePersistenceService&lt;TModel,TDbModel> - (SanteDB.Persistence.Data)
Base persistence services
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## IdentifiedDataPersistenceService&lt;TModel,TDbModel> - (SanteDB.Persistence.Data)
This persistence class represents a persistence service which is capable of storing and maintaining
            an IdentifiedData instance and its equivalent IDbIdentified
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## NonVersionedDataPersistenceService&lt;TModel,TDbModel> - (SanteDB.Persistence.Data)
A class which persists non-versioned data (which has updated timestamps)
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## VersionedAssociationPersistenceService&lt;TModel,TDbModel> - (SanteDB.Persistence.Data)
Abstract class for versioned associations
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## VersionedDataPersistenceService&lt;TModel,TDbModel,TDbKeyModel> - (SanteDB.Persistence.Data)
Persistence service which handles versioned objects
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## SecurityApplicationPersistenceService - (SanteDB.Persistence.Data)
A persistence service that handles security applications

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Security.SecurityApplicationPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SecurityChallengePersistenceService - (SanteDB.Persistence.Data)
Persistence service that stores and retrieves security challenges

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Security.SecurityChallengePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SecurityDevicePersistenceService - (SanteDB.Persistence.Data)
Persistence service that works with SecurityUser instances

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Security.SecurityDevicePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SecurityPolicyPersistenceService - (SanteDB.Persistence.Data)
Persistence service that works with SecurityPolicy objects

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Security.SecurityPolicyPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SecurityProvenancePersistenceService - (SanteDB.Persistence.Data)
Security provenance persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Security.SecurityProvenancePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SecurityRolePersistenceService - (SanteDB.Persistence.Data)
Persistence service that works with SecurityApplication objects

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Security.SecurityRolePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SecurityUserPersistenceService - (SanteDB.Persistence.Data)
Persistence service that works with SecurityApplication objects

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Security.SecurityUserPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MailboxMessagePersistenceService - (SanteDB.Persistence.Data)
Represents a persistence service which can persist the assocation between a mail message and mailbox

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Mail.MailboxMessagePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MailboxPersistenceService - (SanteDB.Persistence.Data)
Persistence service that can persist and handle mailboxes

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Mail.MailboxPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MailMessagePersistenceService - (SanteDB.Persistence.Data)
Mail message persistence service which can handles the persistence of [MailMessage](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Mail_MailMessage.htm) with 
            [DbMailMessage](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Model_Mail_DbMailMessage.htm)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Mail.MailMessagePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ApplicationEntityPersistenceService - (SanteDB.Persistence.Data)
Application entity persistence serivce for application entities

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.ApplicationEntityPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ContainerPersistenceService - (SanteDB.Persistence.Data)
Represents a persistence service that stores/reads containers

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.ContainerPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## DeviceEntityPersistenceService - (SanteDB.Persistence.Data)
Device entity persistence serivce for device entities

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.DeviceEntityPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityAddressComponentPersistenceService - (SanteDB.Persistence.Data)
Entity address component persistence

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.EntityAddressComponentPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityAddressPersistenceService - (SanteDB.Persistence.Data)
A persistence service which operates on [EntityAddress](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Entities_EntityAddress.htm)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.EntityAddressPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityAssociationPersistenceService&lt;TModel,TDbModel> - (SanteDB.Persistence.Data)
A generic implementation of the version association which points at an act
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## EntityDerivedPersistenceService&lt;TEntity,TDbTopLevelTable,TDbEntitySubTable> - (SanteDB.Persistence.Data)
Entity derived persistence service which is responsible for persisting entities which have an intermediary table
### Description
This class is used for higher level entities where the entity is comprised of three sub-tables where 
             links to [DbEntityVersion](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Model_Entities_DbEntityVersion.htm) via
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## EntityDerivedPersistenceService&lt;TEntity,TDbEntitySubTable> - (SanteDB.Persistence.Data)
Entity derived persistence service with one sub entity table
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## EntityDerivedPersistenceService&lt;TEntity> - (SanteDB.Persistence.Data)
Persistence service that is responsible for storing and retrieving entities
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## EntityExtensionPersistenceService - (SanteDB.Persistence.Data)
Entity extension persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.EntityExtensionPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityIdentifierPersistenceService - (SanteDB.Persistence.Data)
Persistence service for entity identifiers

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.EntityIdentifierPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityNameComponentPersistenceService - (SanteDB.Persistence.Data)
Entity name component persistence

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.EntityNameComponentPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityNamePersistenceService - (SanteDB.Persistence.Data)
A persistence service which operates on [EntityAddress](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Entities_EntityAddress.htm)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.EntityNamePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityNotePersistenceService - (SanteDB.Persistence.Data)
Persistence service for entity notes

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.EntityNotePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityPersistenceService - (SanteDB.Persistence.Data)
An persistence service that handles [Entity](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Entities_Entity.htm)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.EntityPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityRelationshipPersistenceService - (SanteDB.Persistence.Data)
A persistence service which handles entity relationships

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.EntityRelationshipPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityTagPersistenceService - (SanteDB.Persistence.Data)
Entity tag persistence

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.EntityTagPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityTelecomPersistenceService - (SanteDB.Persistence.Data)
A persistence service that operates on telecoms

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.EntityTelecomPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ManufacturedMaterialPersistenceService - (SanteDB.Persistence.Data)
A persistence service which is responsible for managing manufactured materials

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.ManufacturedMaterialPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MaterialPersistenceService - (SanteDB.Persistence.Data)
An [EntityDerivedPersistenceService`1](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityDerivedPersistenceService_1.htm) which stores and manages entities

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.MaterialPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## NonPersonLivingSubjectPersistenceService - (SanteDB.Persistence.Data)
Persistence service which is responsible for management of non-person living subjects (like animals, food, substances, viruses, etc.)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.NonPersonLivingSubjectPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## OrganizationPersistenceService - (SanteDB.Persistence.Data)
A persistence service which is able to persist and load [Organization](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Entities_Organization.htm)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.OrganizationPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## PatientPersistenceService - (SanteDB.Persistence.Data)
Persistence service which handles the storage of Patient resources

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.PatientPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## PersonDerivedPersistenceService&lt;TModel,TDbModel> - (SanteDB.Persistence.Data)
A persistence service which is derived from a person persistence
### Description
This class exists to ensure that LanguageCommunication is properly inserted on sub-classes of the Person class
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## PersonLanguageCommunicationPersistenceService - (SanteDB.Persistence.Data)
Persistence service for language of communication

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.PersonLanguageCommunicationPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## PersonPersistenceService - (SanteDB.Persistence.Data)
Persistence service which is responsible for managing persons

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.PersonPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## PlacePersistenceService - (SanteDB.Persistence.Data)
A persistence service class which stores and retrieves places

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.PlacePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## PlaceServicePersistenceService - (SanteDB.Persistence.Data)
Place vs/ service persistence manager

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.PlaceServicePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ProviderPersistenceService - (SanteDB.Persistence.Data)
Persistence service which handles provider classes

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.ProviderPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## UserEntityPersistenceService - (SanteDB.Persistence.Data)
Persistence service which stores and manages

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Entities.UserEntityPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AssigningAuthorityPersistenceService - (SanteDB.Persistence.Data)
Assigning authority persistence

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.AssigningAuthorityPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## CodeSystemPersistenceService - (SanteDB.Persistence.Data)
Code system persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.CodeSystemPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ConceptClassPersistenceService - (SanteDB.Persistence.Data)
Concept class persistence services

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.ConceptClassPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ConceptNamePersistenceService - (SanteDB.Persistence.Data)
Concept name persistence services

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.ConceptNamePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ConceptPersistenceService - (SanteDB.Persistence.Data)
Persistence service for concepts

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.ConceptPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ConceptReferencePersistenceBase&lt;TModel,TDbModel> - (SanteDB.Persistence.Data)
Represents the concept relationship persistence service
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## ConceptReferenceTermPersistenceService - (SanteDB.Persistence.Data)
Concept to Reference term persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.ConceptReferenceTermPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ConceptRelationshipPersistenceService - (SanteDB.Persistence.Data)
Concept relationship persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.ConceptRelationshipPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ConceptRelationshipTypePersistenceService - (SanteDB.Persistence.Data)
Concept relationship type persistnece

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.ConceptRelationshipTypePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ConceptSetCompositionPersistenceService - (SanteDB.Persistence.Data)
Concept set composition persistence

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.ConceptSetCompositionPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ConceptSetPersistenceService - (SanteDB.Persistence.Data)
ConceptSet persistence services for ADO

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.ConceptSetPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ExtensionTypePersistenceService - (SanteDB.Persistence.Data)
Extension type persistence

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.ExtensionTypePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GeoTagPersistenceService - (SanteDB.Persistence.Data)
GEO Tag Persistence

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.GeoTagPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## IdentityDomainPersistenceService - (SanteDB.Persistence.Data)
Assigning authority persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.IdentityDomainPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ProtocolPersistenceService - (SanteDB.Persistence.Data)
Protocol persistence services

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.ProtocolPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ReferenceTermNamePersistenceService - (SanteDB.Persistence.Data)
A persistence service which stores and manages reference term display names

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.ReferenceTermNamePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ReferenceTermPersistenceService - (SanteDB.Persistence.Data)
Persistence service for reference terms.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.ReferenceTermPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## TemplateDefinitionPersistenceService - (SanteDB.Persistence.Data)
Template definition persistence services

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.DataTypes.TemplateDefinitionPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ActAssociationPersistenceService&lt;TModel,TDbModel> - (SanteDB.Persistence.Data)
A generic implementation of the version association which points at an act
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## ActDerivedPersistenceService&lt;TAct,TDbTopLevelTable,TDbActSubTable> - (SanteDB.Persistence.Data)
Entity derived persistence service which is responsible for persisting entities which have an intermediary table
### Description
This class is used for higher level entities where the entity is comprised of three sub-tables where 
             links to [DbActVersion](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Model_Acts_DbActVersion.htm) via
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## ActDerivedPersistenceService&lt;TAct,TDbActSubTable> - (SanteDB.Persistence.Data)
An act derived persistence service where the act has a sub-table storing child data
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## ActDerivedPersistenceService&lt;TAct> - (SanteDB.Persistence.Data)
Persistence service that is responsible for the storing and retrieving of acts
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## ActExtensionPersistenceService - (SanteDB.Persistence.Data)
Entity extension persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.ActExtensionPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ActIdentifierPersistenceService - (SanteDB.Persistence.Data)
Persistence service for act identifiers

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.ActIdentifierPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ActNotePersistenceService - (SanteDB.Persistence.Data)
Persistence service for act notes

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.ActNotePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ActParticipationPersistenceService - (SanteDB.Persistence.Data)
Persistence service between act and act relationship

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.ActParticipationPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ActPersistenceService - (SanteDB.Persistence.Data)
Persistence service which manages acts

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.ActPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ActProtocolPersistenceService - (SanteDB.Persistence.Data)
Act Protocol persistence services

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.ActProtocolPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ActRelationshipPersistenceService - (SanteDB.Persistence.Data)
Persistence service between act and act relationship

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.ActRelationshipPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ActTagPersistenceService - (SanteDB.Persistence.Data)
A tag persistence service for ActTags

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.ActTagPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## CarePathwayDefinitionPersistenceService - (SanteDB.Persistence.Data)
Persistence service for care pathway

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.CarePathwayDefinitionPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## CarePlanPersistenceService - (SanteDB.Persistence.Data)
Persistence service which stores care plans
### Description
The care plan storage has no specific storage requirements for care plans

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.CarePlanPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## CodedObservationPersistenceService - (SanteDB.Persistence.Data)
A [ActDerivedPersistenceService`2](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ActDerivedPersistenceService_2.htm) which stores coded observations

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.CodedObservationPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ControlActPersistenceService - (SanteDB.Persistence.Data)
Persistence service which stores controlling acts

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.ControlActPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## NarrativePersistenceService - (SanteDB.Persistence.Data)
Persistence service that handles narratives

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.NarrativePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ObservationDerivedPersistenceService&lt;TModel,TDbModel> - (SanteDB.Persistence.Data)
Represents a persistence service which stores and retrieves observation based table
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## ObservationPersistenceService - (SanteDB.Persistence.Data)
Generic observation persistence service to handle Observation calls

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.ObservationPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## PatientEncounterArrangementPersistenceService - (SanteDB.Persistence.Data)
Patient encounter arrangement persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.PatientEncounterArrangementPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## PatientEncounterPersistenceService - (SanteDB.Persistence.Data)
Patient encounter based persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.PatientEncounterPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ProcedurePersistenceService - (SanteDB.Persistence.Data)
Persistence service which can store and retrieve patient procedures

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.ProcedurePersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ProtocolPersistenceService - (SanteDB.Persistence.Data)
A [IDataPersistenceService`1](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataPersistenceService_1.htm) which is responsible for the storage and maintenance of [Protocol](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_Protocol.htm) definitions

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.ProtocolPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## QuantityObservationPersistenceService - (SanteDB.Persistence.Data)
An observation persistence service which can manage observations which are quantities (value + unit)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.QuantityObservationPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SubstanceAdministrationPersistenceService - (SanteDB.Persistence.Data)
Class which can persist and manage substance administrations in the database

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.SubstanceAdministrationPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## TextObservationPersistenceService - (SanteDB.Persistence.Data)
Persistence service which can store and retrieve text observations

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.Acts.TextObservationPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyDataPersistenceServiceEx<TModel> : SanteDB.Core.Services.IDataPersistenceServiceEx<TModel> { 
	public String ServiceName => "My own IDataPersistenceServiceEx`1 service";
	/// <summary>
	/// Obsolete all matching data
	/// </summary>
	public void DeleteAll(Expression<Func<TModel,Boolean>> matching,TransactionMode mode,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Touch the specified data
	/// </summary>
	public TModel Touch(Guid key,TransactionMode mode,IPrincipal principal){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDataPersistenceServiceEx&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataPersistenceServiceEx_1.htm)
* [BaseEntityDataPersistenceService&lt;TModel,TDbModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_BaseEntityDataPersistenceService_2.htm)
* [BasePersistenceService&lt;TModel,TDbModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_BasePersistenceService_2.htm)
* [IdentifiedDataPersistenceService&lt;TModel,TDbModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_IdentifiedDataPersistenceService_2.htm)
* [NonVersionedDataPersistenceService&lt;TModel,TDbModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_NonVersionedDataPersistenceService_2.htm)
* [VersionedAssociationPersistenceService&lt;TModel,TDbModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_VersionedAssociationPersistenceService_2.htm)
* [VersionedDataPersistenceService&lt;TModel,TDbModel,TDbKeyModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_VersionedDataPersistenceService_3.htm)
* [SecurityApplicationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Security_SecurityApplicationPersistenceService.htm)
* [SecurityChallengePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Security_SecurityChallengePersistenceService.htm)
* [SecurityDevicePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Security_SecurityDevicePersistenceService.htm)
* [SecurityPolicyPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Security_SecurityPolicyPersistenceService.htm)
* [SecurityProvenancePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Security_SecurityProvenancePersistenceService.htm)
* [SecurityRolePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Security_SecurityRolePersistenceService.htm)
* [SecurityUserPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Security_SecurityUserPersistenceService.htm)
* [MailboxMessagePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Mail_MailboxMessagePersistenceService.htm)
* [MailboxPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Mail_MailboxPersistenceService.htm)
* [MailMessagePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Mail_MailMessagePersistenceService.htm)
* [ApplicationEntityPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_ApplicationEntityPersistenceService.htm)
* [ContainerPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_ContainerPersistenceService.htm)
* [DeviceEntityPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_DeviceEntityPersistenceService.htm)
* [EntityAddressComponentPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityAddressComponentPersistenceService.htm)
* [EntityAddressPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityAddressPersistenceService.htm)
* [EntityAssociationPersistenceService&lt;TModel,TDbModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityAssociationPersistenceService_2.htm)
* [EntityDerivedPersistenceService&lt;TEntity,TDbTopLevelTable,TDbEntitySubTable> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityDerivedPersistenceService_3.htm)
* [EntityDerivedPersistenceService&lt;TEntity,TDbEntitySubTable> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityDerivedPersistenceService_2.htm)
* [EntityDerivedPersistenceService&lt;TEntity> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityDerivedPersistenceService_1.htm)
* [EntityExtensionPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityExtensionPersistenceService.htm)
* [EntityIdentifierPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityIdentifierPersistenceService.htm)
* [EntityNameComponentPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityNameComponentPersistenceService.htm)
* [EntityNamePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityNamePersistenceService.htm)
* [EntityNotePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityNotePersistenceService.htm)
* [EntityPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityPersistenceService.htm)
* [EntityRelationshipPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityRelationshipPersistenceService.htm)
* [EntityTagPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityTagPersistenceService.htm)
* [EntityTelecomPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_EntityTelecomPersistenceService.htm)
* [ManufacturedMaterialPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_ManufacturedMaterialPersistenceService.htm)
* [MaterialPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_MaterialPersistenceService.htm)
* [NonPersonLivingSubjectPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_NonPersonLivingSubjectPersistenceService.htm)
* [OrganizationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_OrganizationPersistenceService.htm)
* [PatientPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_PatientPersistenceService.htm)
* [PersonDerivedPersistenceService&lt;TModel,TDbModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_PersonDerivedPersistenceService_2.htm)
* [PersonLanguageCommunicationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_PersonLanguageCommunicationPersistenceService.htm)
* [PersonPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_PersonPersistenceService.htm)
* [PlacePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_PlacePersistenceService.htm)
* [PlaceServicePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_PlaceServicePersistenceService.htm)
* [ProviderPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_ProviderPersistenceService.htm)
* [UserEntityPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Entities_UserEntityPersistenceService.htm)
* [AssigningAuthorityPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_AssigningAuthorityPersistenceService.htm)
* [CodeSystemPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_CodeSystemPersistenceService.htm)
* [ConceptClassPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_ConceptClassPersistenceService.htm)
* [ConceptNamePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_ConceptNamePersistenceService.htm)
* [ConceptPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_ConceptPersistenceService.htm)
* [ConceptReferencePersistenceBase&lt;TModel,TDbModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_ConceptReferencePersistenceBase_2.htm)
* [ConceptReferenceTermPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_ConceptReferenceTermPersistenceService.htm)
* [ConceptRelationshipPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_ConceptRelationshipPersistenceService.htm)
* [ConceptRelationshipTypePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_ConceptRelationshipTypePersistenceService.htm)
* [ConceptSetCompositionPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_ConceptSetCompositionPersistenceService.htm)
* [ConceptSetPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_ConceptSetPersistenceService.htm)
* [ExtensionTypePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_ExtensionTypePersistenceService.htm)
* [GeoTagPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_GeoTagPersistenceService.htm)
* [IdentityDomainPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_IdentityDomainPersistenceService.htm)
* [ProtocolPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_ProtocolPersistenceService.htm)
* [ReferenceTermNamePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_ReferenceTermNamePersistenceService.htm)
* [ReferenceTermPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_ReferenceTermPersistenceService.htm)
* [TemplateDefinitionPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_DataTypes_TemplateDefinitionPersistenceService.htm)
* [ActAssociationPersistenceService&lt;TModel,TDbModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ActAssociationPersistenceService_2.htm)
* [ActDerivedPersistenceService&lt;TAct,TDbTopLevelTable,TDbActSubTable> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ActDerivedPersistenceService_3.htm)
* [ActDerivedPersistenceService&lt;TAct,TDbActSubTable> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ActDerivedPersistenceService_2.htm)
* [ActDerivedPersistenceService&lt;TAct> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ActDerivedPersistenceService_1.htm)
* [ActExtensionPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ActExtensionPersistenceService.htm)
* [ActIdentifierPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ActIdentifierPersistenceService.htm)
* [ActNotePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ActNotePersistenceService.htm)
* [ActParticipationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ActParticipationPersistenceService.htm)
* [ActPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ActPersistenceService.htm)
* [ActProtocolPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ActProtocolPersistenceService.htm)
* [ActRelationshipPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ActRelationshipPersistenceService.htm)
* [ActTagPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ActTagPersistenceService.htm)
* [CarePathwayDefinitionPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_CarePathwayDefinitionPersistenceService.htm)
* [CarePlanPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_CarePlanPersistenceService.htm)
* [CodedObservationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_CodedObservationPersistenceService.htm)
* [ControlActPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ControlActPersistenceService.htm)
* [NarrativePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_NarrativePersistenceService.htm)
* [ObservationDerivedPersistenceService&lt;TModel,TDbModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ObservationDerivedPersistenceService_2.htm)
* [ObservationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ObservationPersistenceService.htm)
* [PatientEncounterArrangementPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_PatientEncounterArrangementPersistenceService.htm)
* [PatientEncounterPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_PatientEncounterPersistenceService.htm)
* [ProcedurePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ProcedurePersistenceService.htm)
* [ProtocolPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_ProtocolPersistenceService.htm)
* [QuantityObservationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_QuantityObservationPersistenceService.htm)
* [SubstanceAdministrationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_SubstanceAdministrationPersistenceService.htm)
* [TextObservationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_Acts_TextObservationPersistenceService.htm)

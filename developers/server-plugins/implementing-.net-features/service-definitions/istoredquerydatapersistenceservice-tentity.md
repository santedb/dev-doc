`IStoredQueryDataPersistenceService&lt;TEntity>` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a data persistence provider that can store and continue queries

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Query|IEnumerable&lt;TEntity>|*Expression&lt;Func&lt;TEntity,Boolean>>* **query**<br/>*Guid* **queryId**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalCount**<br/>*IPrincipal* **overrideAuthContext**<br/>*ModelSort`1[]* **orderBy**|Queries or continues a query|

# Implementations


## ADO.NET Generic Persistence Provider - (SanteDB.Persistence.Data.ADO)
Represents a data persistence service which stores data in the local SQLite data store
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## EntityIdentifierPersistenceService - (SanteDB.Persistence.Data.ADO)
Entity identifier persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.EntityIdentifierPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ActDerivedPersistenceService&lt;TModel,TData> - (SanteDB.Persistence.Data.ADO)
Represents a persistence service which is derived from an act
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## ActDerivedPersistenceService&lt;TModel,TData,TQueryReturn> - (SanteDB.Persistence.Data.ADO)
Represents a persistence service which is derived from an act
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## ActParticipationPersistenceService - (SanteDB.Persistence.Data.ADO)
Act participation persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ActParticipationPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ActPersistenceService - (SanteDB.Persistence.Data.ADO)
Represents a persistence service which persists ACT classes

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ActPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ActRelationshipPersistenceService - (SanteDB.Persistence.Data.ADO)
Represents a persister which is a act relationship

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ActRelationshipPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MailMessagePersistenceService - (SanteDB.Persistence.Data.ADO)
Represents an alert persistence service.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.MailMessagePersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ApplicationEntityPersistenceService - (SanteDB.Persistence.Data.ADO)
Represents the persistence service for application eneities

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ApplicationEntityPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AssigningAuthorityPersistenceService - (SanteDB.Persistence.Data.ADO)
Assigning authority persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.AssigningAuthorityPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## BaseDataPersistenceService&lt;TModel,TDomain> - (SanteDB.Persistence.Data.ADO)
Base persistence service
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## BaseDataPersistenceService&lt;TModel,TDomain,TQueryResult> - (SanteDB.Persistence.Data.ADO)
Base data persistence service
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## BundlePersistenceService - (SanteDB.Persistence.Data.ADO)
Bundle persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.BundlePersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ConceptPersistenceService - (SanteDB.Persistence.Data.ADO)
Concept persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ConceptPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ConceptNamePersistenceService - (SanteDB.Persistence.Data.ADO)
Persistence service for concept names

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ConceptNamePersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ConceptSetPersistenceService - (SanteDB.Persistence.Data.ADO)
Persistence service for ConceptSets

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ConceptSetPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ControlActPersistenceService - (SanteDB.Persistence.Data.ADO)
Control act persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ControlActPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## CorePersistenceService&lt;TModel,TDomain,TQueryReturn> - (SanteDB.Persistence.Data.ADO)
Core persistence service which contains helpful functions
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## DeviceEntityPersistenceService - (SanteDB.Persistence.Data.ADO)
Represents a persistence service for a device entity

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.DeviceEntityPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EncounterPersistenceService - (SanteDB.Persistence.Data.ADO)
Persistence class which persists encounters

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.EncounterPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityAddressPersistenceService - (SanteDB.Persistence.Data.ADO)
Represents a persistence service for entity addresses

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.EntityAddressPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityAddressComponentPersistenceService - (SanteDB.Persistence.Data.ADO)
Entity address component persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.EntityAddressComponentPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityDerivedPersistenceService&lt;TModel,TData> - (SanteDB.Persistence.Data.ADO)
TODO: Document this
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## EntityDerivedPersistenceService&lt;TModel,TData,TQueryReturn> - (SanteDB.Persistence.Data.ADO)
Entity derived persistence services
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## EntityNamePersistenceService - (SanteDB.Persistence.Data.ADO)
Entity name persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.EntityNamePersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityNameComponentPersistenceService - (SanteDB.Persistence.Data.ADO)
Represents an entity name component persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.EntityNameComponentPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityPersistenceService - (SanteDB.Persistence.Data.ADO)
Entity persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.EntityPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityRelationshipPersistenceService - (SanteDB.Persistence.Data.ADO)
Entity relationship persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.EntityRelationshipPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## IdentifiedPersistenceService&lt;TModel,TDomain> - (SanteDB.Persistence.Data.ADO)
Generic persistnece service for identified entities
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## IdentifiedPersistenceService&lt;TModel,TDomain,TQueryResult> - (SanteDB.Persistence.Data.ADO)
Generic persistence service which can persist between two simple types.
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## IdentifierTypePersistenceService - (SanteDB.Persistence.Data.ADO)
Represents a persistence service for an identifier type.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.IdentifierTypePersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ManufacturedMaterialPersistenceService - (SanteDB.Persistence.Data.ADO)
Manufactured material persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ManufacturedMaterialPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MaterialPersistenceService - (SanteDB.Persistence.Data.ADO)
Persistence service for matrials

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.MaterialPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ObservationPersistenceService - (SanteDB.Persistence.Data.ADO)
Persistence class for observations

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ObservationPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## TextObservationPersistenceService - (SanteDB.Persistence.Data.ADO)
Text observation service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.TextObservationPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## CodedObservationPersistenceService - (SanteDB.Persistence.Data.ADO)
Coded observation service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.CodedObservationPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## QuantityObservationPersistenceService - (SanteDB.Persistence.Data.ADO)
Quantity observation persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.QuantityObservationPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## OrganizationPersistenceService - (SanteDB.Persistence.Data.ADO)
Represents an organization persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.OrganizationPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## PatientPersistenceService - (SanteDB.Persistence.Data.ADO)
Persistence service which is used to persist patients

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.PatientPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## PersonPersistenceService - (SanteDB.Persistence.Data.ADO)
Person persistence service
### Description
This is a little different than the other persisters as we have to 
            persist half the object in one set of tables ane the other fields in this
            table

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.PersonPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## PlacePersistenceService - (SanteDB.Persistence.Data.ADO)
Represents a persister which persists places

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.PlacePersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ProtocolPersistenceService - (SanteDB.Persistence.Data.ADO)
Protocol service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ProtocolPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ProviderPersistenceService - (SanteDB.Persistence.Data.ADO)
Provider persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ProviderPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ReferenceTermNamePersistenceService - (SanteDB.Persistence.Data.ADO)
Represents a reference term name persistence service.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ReferenceTermNamePersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SecurityProvenancePersistenceService - (SanteDB.Persistence.Data.ADO)
Security provenance service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.SecurityProvenancePersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SecurityApplicationPersistenceService - (SanteDB.Persistence.Data.ADO)
Security user persistence

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.SecurityApplicationPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SecurityDevicePersistenceService - (SanteDB.Persistence.Data.ADO)
Security user persistence

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.SecurityDevicePersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SecurityPolicyPersistenceService - (SanteDB.Persistence.Data.ADO)
Represents a persistence service for security policies.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.SecurityPolicyPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SecurityRolePersistenceService - (SanteDB.Persistence.Data.ADO)
Security user persistence

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.SecurityRolePersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SecurityUserPersistenceService - (SanteDB.Persistence.Data.ADO)
Security user persistence

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.SecurityUserPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SimpleVersionedEntityPersistenceService&lt;TModel,TData,TQueryReturn,TRootEntity> - (SanteDB.Persistence.Data.ADO)
Represents a simple versioned entity persistence service
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## ProcedurePersistenceService - (SanteDB.Persistence.Data.ADO)
Represents a persistence service for substance administrations

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ProcedurePersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SubstanceAdministrationPersistenceService - (SanteDB.Persistence.Data.ADO)
Represents a persistence service for substance administrations

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.SubstanceAdministrationPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## UserEntityPersistenceService - (SanteDB.Persistence.Data.ADO)
Represents a persister that can read/write user entities

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.UserEntityPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## VersionedDataPersistenceService&lt;TModel,TDomain,TDomainKey> - (SanteDB.Persistence.Data.ADO)
Versioned domain data
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## ReferenceTermPersistenceService - (SanteDB.Persistence.Data.ADO)
Represents a reference term persistence service.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ReferenceTermPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GenericBasePersistenceService&lt;TModel,TDomain> - (SanteDB.Persistence.Data.ADO)
TODO: Document this
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## GenericIdentityPersistenceService&lt;TModel,TDomain> - (SanteDB.Persistence.Data.ADO)
TODO: Document this
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## GenericBaseAssociationPersistenceService&lt;TModel,TDomain> - (SanteDB.Persistence.Data.ADO)
TODO: Document this
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## GenericBaseVersionedAssociationPersistenceService&lt;TModel,TDomain> - (SanteDB.Persistence.Data.ADO)
TODO: Document this
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## GenericIdentityAssociationPersistenceService&lt;TModel,TDomain> - (SanteDB.Persistence.Data.ADO)
TODO: Document this
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## GenericIdentityVersionedAssociationPersistenceService&lt;TModel,TDomain> - (SanteDB.Persistence.Data.ADO)
TODO: Document this
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyStoredQueryDataPersistenceService<TEntity> : SanteDB.Core.Services.IStoredQueryDataPersistenceService<TEntity> { 
	public String ServiceName => "My own IStoredQueryDataPersistenceService`1 service";
	/// <summary>
	/// Queries or continues a query
	/// </summary>
	public IEnumerable<TEntity> Query(Expression<Func<TEntity,Boolean>> query,Guid queryId,Int32 offset,Nullable<Int32> count,Int32& totalCount,IPrincipal overrideAuthContext,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IStoredQueryDataPersistenceService&lt;TEntity> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IStoredQueryDataPersistenceService_1.htm)
* [AdoBasePersistenceService&lt;TData> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoBasePersistenceService_1.htm)
* [EntityIdentifierPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_EntityIdentifierPersistenceService.htm)
* [ActDerivedPersistenceService&lt;TModel,TData> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ActDerivedPersistenceService_2.htm)
* [ActDerivedPersistenceService&lt;TModel,TData,TQueryReturn> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ActDerivedPersistenceService_3.htm)
* [ActParticipationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ActParticipationPersistenceService.htm)
* [ActPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ActPersistenceService.htm)
* [ActRelationshipPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ActRelationshipPersistenceService.htm)
* [MailMessagePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_MailMessagePersistenceService.htm)
* [ApplicationEntityPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ApplicationEntityPersistenceService.htm)
* [AssigningAuthorityPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_AssigningAuthorityPersistenceService.htm)
* [BaseDataPersistenceService&lt;TModel,TDomain> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_BaseDataPersistenceService_2.htm)
* [BaseDataPersistenceService&lt;TModel,TDomain,TQueryResult> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_BaseDataPersistenceService_3.htm)
* [BundlePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_BundlePersistenceService.htm)
* [ConceptPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ConceptPersistenceService.htm)
* [ConceptNamePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ConceptNamePersistenceService.htm)
* [ConceptSetPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ConceptSetPersistenceService.htm)
* [ControlActPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ControlActPersistenceService.htm)
* [CorePersistenceService&lt;TModel,TDomain,TQueryReturn> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_CorePersistenceService_3.htm)
* [DeviceEntityPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_DeviceEntityPersistenceService.htm)
* [EncounterPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_EncounterPersistenceService.htm)
* [EntityAddressPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_EntityAddressPersistenceService.htm)
* [EntityAddressComponentPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_EntityAddressComponentPersistenceService.htm)
* [EntityDerivedPersistenceService&lt;TModel,TData> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_EntityDerivedPersistenceService_2.htm)
* [EntityDerivedPersistenceService&lt;TModel,TData,TQueryReturn> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_EntityDerivedPersistenceService_3.htm)
* [EntityNamePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_EntityNamePersistenceService.htm)
* [EntityNameComponentPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_EntityNameComponentPersistenceService.htm)
* [EntityPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_EntityPersistenceService.htm)
* [EntityRelationshipPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_EntityRelationshipPersistenceService.htm)
* [IdentifiedPersistenceService&lt;TModel,TDomain> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_IdentifiedPersistenceService_2.htm)
* [IdentifiedPersistenceService&lt;TModel,TDomain,TQueryResult> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_IdentifiedPersistenceService_3.htm)
* [IdentifierTypePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_IdentifierTypePersistenceService.htm)
* [ManufacturedMaterialPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ManufacturedMaterialPersistenceService.htm)
* [MaterialPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_MaterialPersistenceService.htm)
* [ObservationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ObservationPersistenceService.htm)
* [TextObservationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_TextObservationPersistenceService.htm)
* [CodedObservationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_CodedObservationPersistenceService.htm)
* [QuantityObservationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_QuantityObservationPersistenceService.htm)
* [OrganizationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_OrganizationPersistenceService.htm)
* [PatientPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_PatientPersistenceService.htm)
* [PersonPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_PersonPersistenceService.htm)
* [PlacePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_PlacePersistenceService.htm)
* [ProtocolPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ProtocolPersistenceService.htm)
* [ProviderPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ProviderPersistenceService.htm)
* [ReferenceTermNamePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ReferenceTermNamePersistenceService.htm)
* [SecurityProvenancePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_SecurityProvenancePersistenceService.htm)
* [SecurityApplicationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_SecurityApplicationPersistenceService.htm)
* [SecurityDevicePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_SecurityDevicePersistenceService.htm)
* [SecurityPolicyPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_SecurityPolicyPersistenceService.htm)
* [SecurityRolePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_SecurityRolePersistenceService.htm)
* [SecurityUserPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_SecurityUserPersistenceService.htm)
* [SimpleVersionedEntityPersistenceService&lt;TModel,TData,TQueryReturn,TRootEntity> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_SimpleVersionedEntityPersistenceService_4.htm)
* [ProcedurePersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ProcedurePersistenceService.htm)
* [SubstanceAdministrationPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_SubstanceAdministrationPersistenceService.htm)
* [UserEntityPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_UserEntityPersistenceService.htm)
* [VersionedDataPersistenceService&lt;TModel,TDomain,TDomainKey> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_VersionedDataPersistenceService_3.htm)
* [ReferenceTermPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_Persistence_ReferenceTermPersistenceService.htm)
* [GenericBasePersistenceService&lt;TModel,TDomain> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoServiceFactory+GenericBasePersistenceService_2.htm)
* [GenericIdentityPersistenceService&lt;TModel,TDomain> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoServiceFactory+GenericIdentityPersistenceService_2.htm)
* [GenericBaseAssociationPersistenceService&lt;TModel,TDomain> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoServiceFactory+GenericBaseAssociationPersistenceService_2.htm)
* [GenericBaseVersionedAssociationPersistenceService&lt;TModel,TDomain> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoServiceFactory+GenericBaseVersionedAssociationPersistenceService_2.htm)
* [GenericIdentityAssociationPersistenceService&lt;TModel,TDomain> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoServiceFactory+GenericIdentityAssociationPersistenceService_2.htm)
* [GenericIdentityVersionedAssociationPersistenceService&lt;TModel,TDomain> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoServiceFactory+GenericIdentityVersionedAssociationPersistenceService_2.htm)

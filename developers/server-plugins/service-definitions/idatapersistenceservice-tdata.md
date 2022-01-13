IDataPersistenceService&lt;TData> (IDataPersistenceService&lt;TData> in SanteDB.Core.Api)

# Summary
Represents a data persistence service which is capable of storing and retrieving data
            to/from a data store

# Events

|Event|Type|Description|
|-|-|-|
|Inserted|EventHandler&lt;DataPersistedEventArgs&lt;TData>>|Occurs when inserted.|
|Inserting|EventHandler&lt;DataPersistingEventArgs&lt;TData>>|Occurs when inserting.|
|Updated|EventHandler&lt;DataPersistedEventArgs&lt;TData>>|Occurs when updated.|
|Updating|EventHandler&lt;DataPersistingEventArgs&lt;TData>>|Occurs when updating.|
|Obsoleted|EventHandler&lt;DataPersistedEventArgs&lt;TData>>|Occurs when obsoleted.|
|Obsoleting|EventHandler&lt;DataPersistingEventArgs&lt;TData>>|Occurs when obsoleting.|
|Queried|EventHandler&lt;QueryResultEventArgs&lt;TData>>|Occurs when queried.|
|Querying|EventHandler&lt;QueryRequestEventArgs&lt;TData>>|Occurs when querying.|
|Retrieving|EventHandler&lt;DataRetrievingEventArgs&lt;TData>>|Data is being retrieved|
|Retrieved|EventHandler&lt;DataRetrievedEventArgs&lt;TData>>|Fired when data has been retrieved|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Insert|TData|*TData* **data**<br/>*TransactionMode* **mode**<br/>*IPrincipal* **principal**|Insert the specified data.|
|Update|TData|*TData* **data**<br/>*TransactionMode* **mode**<br/>*IPrincipal* **principal**|Update the specified data|
|Obsolete|TData|*TData* **data**<br/>*TransactionMode* **mode**<br/>*IPrincipal* **principal**|Obsolete the specified identified data|
|Get|TData|*Guid* **key**<br/>*Nullable&lt;Guid>* **versionKey**<br/>*Boolean* **loadFast**<br/>*IPrincipal* **principal**|Get the object specified .|
|Query|IEnumerable&lt;TData>|*Expression&lt;Func&lt;TData,Boolean>>* **query**<br/>*IPrincipal* **principal**|Query the specified data|
|Query|IEnumerable&lt;TData>|*Expression&lt;Func&lt;TData,Boolean>>* **query**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**<br/>*IPrincipal* **principal**<br/>*ModelSort`1[]* **orderBy**|Query the specified data|
|Count|Int64|*Expression&lt;Func&lt;TData,Boolean>>* **p**<br/>*IPrincipal* **authContext**|Performs a fast count|

# Implementations


## ADO.NET Audit Repository - (SanteDB.Persistence.Auditing.ADO)
Represents a service which is responsible for the storage of audits

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Auditing.ADO.Services.AdoAuditRepositoryService, SanteDB.Persistence.Auditing.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ADO.NET Generic Persistence Provider - (SanteDB.Persistence.Data.ADO)
Represents a data persistence service which stores data in the local SQLite data store

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoBasePersistenceService`1, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

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

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ActDerivedPersistenceService`2, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ActDerivedPersistenceService&lt;TModel,TData,TQueryReturn> - (SanteDB.Persistence.Data.ADO)
Represents a persistence service which is derived from an act

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.ActDerivedPersistenceService`3, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

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

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.BaseDataPersistenceService`2, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## BaseDataPersistenceService&lt;TModel,TDomain,TQueryResult> - (SanteDB.Persistence.Data.ADO)
Base data persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.BaseDataPersistenceService`3, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

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

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.CorePersistenceService`3, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

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

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.EntityDerivedPersistenceService`2, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## EntityDerivedPersistenceService&lt;TModel,TData,TQueryReturn> - (SanteDB.Persistence.Data.ADO)
Entity derived persistence services

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.EntityDerivedPersistenceService`3, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

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

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.IdentifiedPersistenceService`2, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## IdentifiedPersistenceService&lt;TModel,TDomain,TQueryResult> - (SanteDB.Persistence.Data.ADO)
Generic persistence service which can persist between two simple types.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.IdentifiedPersistenceService`3, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

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

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.SimpleVersionedEntityPersistenceService`4, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

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

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.Persistence.VersionedDataPersistenceService`3, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

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

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoServiceFactory+GenericBasePersistenceService`2, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GenericIdentityPersistenceService&lt;TModel,TDomain> - (SanteDB.Persistence.Data.ADO)
TODO: Document this

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoServiceFactory+GenericIdentityPersistenceService`2, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GenericBaseAssociationPersistenceService&lt;TModel,TDomain> - (SanteDB.Persistence.Data.ADO)
TODO: Document this

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoServiceFactory+GenericBaseAssociationPersistenceService`2, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GenericBaseVersionedAssociationPersistenceService&lt;TModel,TDomain> - (SanteDB.Persistence.Data.ADO)
TODO: Document this

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoServiceFactory+GenericBaseVersionedAssociationPersistenceService`2, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GenericIdentityAssociationPersistenceService&lt;TModel,TDomain> - (SanteDB.Persistence.Data.ADO)
TODO: Document this

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoServiceFactory+GenericIdentityAssociationPersistenceService`2, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GenericIdentityVersionedAssociationPersistenceService&lt;TModel,TDomain> - (SanteDB.Persistence.Data.ADO)
TODO: Document this

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoServiceFactory+GenericIdentityVersionedAssociationPersistenceService`2, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## E-Mail Diagnostic (Bug) Report Submission - (SanteDB.Persistence.Diagnostics.Email)
TODO: Document this

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Diagnostics.Email.DiagnosticReportPersistenceService, SanteDB.Persistence.Diagnostics.Email, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## JIRA Based Diagnostic (Bug) Report Submissions - (SanteDB.Persistence.Diagnostics.Jira)
TODO: Document this

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Diagnostics.Jira.DiagnosticReportPersistenceService, SanteDB.Persistence.Diagnostics.Jira, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyDataPersistenceService<TData> : SanteDB.Core.Services.IDataPersistenceService<TData> { 
	public String ServiceName => "My own IDataPersistenceService`1 service";
	/// <summary>
	/// Occurs when inserted.
	/// </summary>
	public event EventHandler<DataPersistedEventArgs<TData>> Inserted;
	/// <summary>
	/// Occurs when inserting.
	/// </summary>
	public event EventHandler<DataPersistingEventArgs<TData>> Inserting;
	/// <summary>
	/// Occurs when updated.
	/// </summary>
	public event EventHandler<DataPersistedEventArgs<TData>> Updated;
	/// <summary>
	/// Occurs when updating.
	/// </summary>
	public event EventHandler<DataPersistingEventArgs<TData>> Updating;
	/// <summary>
	/// Occurs when obsoleted.
	/// </summary>
	public event EventHandler<DataPersistedEventArgs<TData>> Obsoleted;
	/// <summary>
	/// Occurs when obsoleting.
	/// </summary>
	public event EventHandler<DataPersistingEventArgs<TData>> Obsoleting;
	/// <summary>
	/// Occurs when queried.
	/// </summary>
	public event EventHandler<QueryResultEventArgs<TData>> Queried;
	/// <summary>
	/// Occurs when querying.
	/// </summary>
	public event EventHandler<QueryRequestEventArgs<TData>> Querying;
	/// <summary>
	/// Data is being retrieved
	/// </summary>
	public event EventHandler<DataRetrievingEventArgs<TData>> Retrieving;
	/// <summary>
	/// Fired when data has been retrieved
	/// </summary>
	public event EventHandler<DataRetrievedEventArgs<TData>> Retrieved;
	/// <summary>
	/// Insert the specified data.
	/// </summary>
	public TData Insert(TData data,TransactionMode mode,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Update the specified data
	/// </summary>
	public TData Update(TData data,TransactionMode mode,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Obsolete the specified identified data
	/// </summary>
	public TData Obsolete(TData data,TransactionMode mode,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the object specified .
	/// </summary>
	public TData Get(Guid key,Nullable<Guid> versionKey,Boolean loadFast,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Query the specified data
	/// </summary>
	public IEnumerable<TData> Query(Expression<Func<TData,Boolean>> query,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Query the specified data
	/// </summary>
	public IEnumerable<TData> Query(Expression<Func<TData,Boolean>> query,Int32 offset,Nullable<Int32> count,Int32& totalResults,IPrincipal principal,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Performs a fast count
	/// </summary>
	public Int64 Count(Expression<Func<TData,Boolean>> p,IPrincipal authContext){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDataPersistenceService&lt;TData> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataPersistenceService_1.htm)
* [AdoAuditRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Auditing_ADO_Services_AdoAuditRepositoryService.htm)
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
* [DiagnosticReportPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Diagnostics_Email_DiagnosticReportPersistenceService.htm)
* [DiagnosticReportPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Diagnostics_Jira_DiagnosticReportPersistenceService.htm)

---
description: IServiceImplementation (SanteDB.Core.Api)
---

## Summary
Represents a marker class for a service implementation

## Implementations


### AppletSubscriptionRepository (build-nu)
TODO: Document this

### AppletBiRepository (SanteDB.BI)
Represents a default implementation of a BIS metadata repository which loads definitions from loaded applets

### LocalBiRenderService (SanteDB.BI)
Rendering service which renders reports locally

### RuleServiceBase`1 (SanteDB.BusinessRules.JavaScript)
Represents a rule service base binding

### Applet Based Clinical Protocol Repository (SanteDB.Cdss.Xml)
Applet clinical protocol repository

### Default Policy Enforcement Service (SanteDB.Core.Api)
Local policy enforcement point service

### SECURITY AUDIT SERVICE (SanteDB.Core.Api)
A daemon service which listens to audit sources and forwards them to the auditor

### Simple Care Planning Service (SanteDB.Core.Api)
Represents a care plan service that can bundle protocol acts together 
            based on their start/stop times

### Basic Patching Service (SanteDB.Core.Api)
Represents a simple patch service which can calculate patches and apply them

### SimDataManagementService (SanteDB.Core.Api)
Represents a daemon service that registers a series of merge services which can merge records together

### DataQualityBundleRule (SanteDB.Core.Api)
Represents a bundle data quality rule

### DataQualityBusinessRule`1 (SanteDB.Core.Api)
Represents a single data quality business rule

### DataQualityService (SanteDB.Core.Api)
The data quality service handler

### SimResourceMerger`1 (SanteDB.Core.Api)
TODO: Document this

### AppletSubscriptionRepository (SanteDB.Core.Applets)
An implementation of the ISubscriptionRepository that loads definitions from applets

### AgsService (SanteDB.DisconnectedClient.Ags)
Represents the Applet Gateway Service

### SQLiteAuditRepositoryService (SanteDB.DisconnectedClient.SQLite)
Local audit repository service

### SQLiteDatawarehouse (SanteDB.DisconnectedClient.SQLite)
Represents a simple SQLite ad-hoc data warehouse

### SQLiteQueueManagerService (SanteDB.DisconnectedClient.SQLite)
Queue manager daemon

### SQLite-NET PCL Device Identity Provider (SanteDB.DisconnectedClient.SQLite)
Represents a SQL.NET PCL Device identity provider

### SQLiteIdentityService (SanteDB.DisconnectedClient.SQLite)
Local identity service.

### SQLitePolicyInformationService (SanteDB.DisconnectedClient.SQLite)
Represents a PIP which uses the local data store

### SQLiteRoleProviderService (SanteDB.DisconnectedClient.SQLite)
Local role provider service

### SQLiteSearchIndexService (SanteDB.DisconnectedClient.SQLite)
Search indexing service

### ActDerivedPersistenceService`3 (SanteDB.DisconnectedClient.SQLite)
Represents a persistence service which is derived from an act

### ActParticipationPersistenceService (SanteDB.DisconnectedClient.SQLite)
Act participation persistence service

### ActPersistenceService (SanteDB.DisconnectedClient.SQLite)
Represents a persistence service which persists ACT classes

### ActRelationshipPersistenceService (SanteDB.DisconnectedClient.SQLite)
Represents a persister which is a act relationship

### ApplicationEntityPersistenceService (SanteDB.DisconnectedClient.SQLite)
Represents the persistence service for application eneities

### AuthorityPersistenceService (SanteDB.DisconnectedClient.SQLite)
Represents a persistence service for authorities

### BundlePersistenceService (SanteDB.DisconnectedClient.SQLite)
Represents a bundle persistence service

### ConceptPersistenceService (SanteDB.DisconnectedClient.SQLite)
Concept persistence service

### ConceptSetPersistenceService (SanteDB.DisconnectedClient.SQLite)
Persistence service for ConceptSets

### ControlActPersistenceService (SanteDB.DisconnectedClient.SQLite)
Control act persistence service

### DeviceEntityPersistenceService (SanteDB.DisconnectedClient.SQLite)
Represents a persistence service for a device entity

### EncounterPersistenceService (SanteDB.DisconnectedClient.SQLite)
Persistence class which persists encounters

### EntityAddressPersistenceService (SanteDB.DisconnectedClient.SQLite)
Represents a persistence service for entity addresses

### EntityAddressComponentPersistenceService (SanteDB.DisconnectedClient.SQLite)
Entity address component persistence service

### EntityDerivedPersistenceService`3 (SanteDB.DisconnectedClient.SQLite)
Entity derived persistence services

### EntityNamePersistenceService (SanteDB.DisconnectedClient.SQLite)
Entity name persistence service

### EntityNameComponentPersistenceService (SanteDB.DisconnectedClient.SQLite)
Entity address component persistence service

### EntityPersistenceService (SanteDB.DisconnectedClient.SQLite)
Entity persistence service

### EntityRelationshipPersistenceService (SanteDB.DisconnectedClient.SQLite)
Entity relationship persistence service

### ManufacturedMaterialPersistenceService (SanteDB.DisconnectedClient.SQLite)
Manufactured material persistence service

### MaterialPersistenceService (SanteDB.DisconnectedClient.SQLite)
Persistence service for matrials

### TextObservationPersistenceService (SanteDB.DisconnectedClient.SQLite)
Text observation service

### CodedObservationPersistenceService (SanteDB.DisconnectedClient.SQLite)
Coded observation service

### QuantityObservationPersistenceService (SanteDB.DisconnectedClient.SQLite)
Quantity observation persistence service

### OrganizationPersistenceService (SanteDB.DisconnectedClient.SQLite)
Represents an organization persistence service

### PatientPersistenceService (SanteDB.DisconnectedClient.SQLite)
Persistence service which is used to persist patients

### PersonPersistenceService (SanteDB.DisconnectedClient.SQLite)
Person persistence service

### PlacePersistenceService (SanteDB.DisconnectedClient.SQLite)
Represents a persister which persists places

### ProviderPersistenceService (SanteDB.DisconnectedClient.SQLite)
Provider persistence service

### ReferenceTermNamePersister (SanteDB.DisconnectedClient.SQLite)
Persistence service for reftermname

### ReferenceTermPersistenceService (SanteDB.DisconnectedClient.SQLite)
Represents a reference term persistence service.

### SecurityUserPersistenceService (SanteDB.DisconnectedClient.SQLite)
Security user persistence

### SecurityRolePersistenceService (SanteDB.DisconnectedClient.SQLite)
Security user persistence

### SecurityDevicePersistenceService (SanteDB.DisconnectedClient.SQLite)
Security user persistence

### SecurityApplicationPersistenceService (SanteDB.DisconnectedClient.SQLite)
Security user persistence

### SubstanceAdministrationPersistenceService (SanteDB.DisconnectedClient.SQLite)
Represents a persistence service for substance administrations

### UserEntityPersistenceService (SanteDB.DisconnectedClient.SQLite)
Represents a persister that can read/write user entities

### MdmDataManager (SanteDB.DisconnectedClient.SQLite)
When synchronizing with a server which has MDM enabled.

### SQLiteMailPersistenceService (SanteDB.DisconnectedClient.SQLite)
Alert persistence service

### SQLiteConnectionManager (SanteDB.DisconnectedClient.SQLite)
SQLiteConnectionManager

### GenericVersionedPersistenceService`2 (SanteDB.DisconnectedClient.SQLite)
TODO: Document this

### GenericBasePersistenceService`2 (SanteDB.DisconnectedClient.SQLite)
TODO: Document this

### GenericIdentityPersistenceService`2 (SanteDB.DisconnectedClient.SQLite)
TODO: Document this

### GenericIdentityAssociationPersistenceService`2 (SanteDB.DisconnectedClient.SQLite)
TODO: Document this

### AppletMatchConfigurationProvider (SanteDB.Matcher)
Applet match configuration provider loads match configurations from available applets

### AssemblyMatchConfigurationProvider (SanteDB.Matcher)
File based match configuration provider

### SanteMatch Deterministic Matcher (SanteDB.Matcher)
Represents a deterministic record matching service

### SanteMatch Probabalistic Match Service (SanteDB.Matcher)
Represents a probabalistic record matching service

### OpenAPI Metadata Exchange (SanteDB.Messaging.Metadata)
TODO: Document this

### BIS REST Daemon (SanteDB.Rest.BIS)
Represents a message handler for the BIS
## Example Implementation
```
None
```

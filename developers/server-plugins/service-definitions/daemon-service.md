`IDaemonService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Defines a service which follows the daemon service pattern ([](https://help.santesuite.org/developers/server-plugins/implementing-.net-features/daemon-services))

## Description
In SanteDB (and OpenIZ) a daemon service is an actively executed service which is started on application host start and torn down/stopped on application
             context shutdown (or when initiated by a user). 

The [Start](#Start) method is invoked on startup. It is expected that implementer of this class
             will raise the [Starting](#Starting) event to signal to other services in the application context that this particular service is starting. Once the initialization process
             is complete, the implementation should call the [Started](#Started) event to signal this service has completed its necessary start, before returning true from the start method.
             This behavior allows chaining of dependent services together (i.e. don't start until after start of another service)

On service teardown the [Stop](#Stop) method is called, again it is expected that implementers will raise [Stopping](#Stopping) and then [Stopped](#Stopped)

If the daemon also implements the .NET [IDisposable](https://docs.microsoft.com/en-us/dotnet/api/system.idisposable) interface, then the Dispose method is called after service shutdown.

# Events

|Event|Type|Description|
|-|-|-|
|Starting|EventHandler|Fired when the daemon service has commenced start but has not yet finished|
|Started|EventHandler|Fired when the daemon service has completed it start procedure.|
|Stopping|EventHandler|Fired when the daemon service has commenced stop but has not yet been fully shut down.|
|Stopped|EventHandler|Fired when the daemon has completed its stop procedure|

# Properties

|Property|Type|Access|Description|
|-|-|-|-|
|IsRunning|Boolean|R|Indicates whether the daemon service is running|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Start|Boolean|*none*|TODO|
|Stop|Boolean|*none*|TODO|

# Implementations


## OAuth 2.0 Messaging Service - (SanteDB.Authentication.OAuth2)
Represents a [IApiEndpointProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Interop_IApiEndpointProvider.htm) which serves OpenID Connect and 
            OAUTH requests
### Description
This service is responsible for starting and maintaining the [OAuthTokenBehavior](http://santesuite.org/assets/doc/net/html/T_SanteDB_Authentication_OAuth2_Rest_OAuthTokenBehavior.htm) REST service which 
            is responsible for supporting SanteDB's [OpenID Connect](https://help.santesuite.org/developers/service-apis/openid-connect) interface

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Authentication.OAuth2.OAuthMessageHandler, SanteDB.Authentication.OAuth2, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Memory Cache Service - (SanteDB.Caching.Memory)
Implementation of the [IDataCachingService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataCachingService.htm) which uses the in-process memory to cache objects
### Description
The memory cache service uses the [MemoryCache](https://docs.microsoft.com/en-us/dotnet/api/system.runtime.caching.memorycache) class as a backing cache
            for the SanteDB host instance. This caching provider provides benefits over a common, shared cache like REDIS in that:

* It does not require the setup of a third-party service to operate
* The cache objects are directly accessed and not serialized
* The cache objects are protected within the host process memory
* The access is very fast - there is no interconnection with another process


This cache service should only be used in cases when there is a single SanteDB server and there is no need
            for sharing cache objects between application services.

This class uses the TTL setting from the [MemoryCacheConfigurationSection](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Memory_Configuration_MemoryCacheConfigurationSection.htm) to determine the length of time
            that cache entries are valid

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Caching.Memory.MemoryCacheService, SanteDB.Caching.Memory, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## RedisAdhocCache - (SanteDB.Caching.Redis)
An implementation of the [IAdhocCacheService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IAdhocCacheService.htm) which uses REDIS as the cache provider
### Description
This implementation of the REDIS ad-hoc cache provider serializes any data passed via [TimeSpan})](#TimeSpan})) to a JSON representation, then
            compresses (optional) the data and stores it in REDIS as a simple string

The data is stored in database 3 of the REDIS server

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Caching.Redis.RedisAdhocCache, SanteDB.Caching.Redis, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## REDIS Data Caching Service - (SanteDB.Caching.Redis)
An implementation of the [IDataCachingService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataCachingService.htm) which uses REDIS
### Description
This implementation of the caching service uses the XMLSerializer in .NET to serialize any object passed in
            via the [IdentifiedData)](#IdentifiedData)) method. The data is then compressed (if configured) and sent to the
            configured REDIS server.

The use of the .NET XML serializer over the Newtonsoft JSON serializer for caching was chosen since the
            serializer operates on streams (saves string conversions) and pre-compiles the serialization classes on .NET Framework implementations
            (Mono implementations use relfection)

The caching data is stored in database 1 of the REDIS server.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Caching.Redis.RedisCacheService, SanteDB.Caching.Redis, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## REDIS Query Persistence Service - (SanteDB.Caching.Redis)
An implementation of the [IQueryPersistenceService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IQueryPersistenceService.htm) which usees REDIS for its stateful result set
### Description
This persistence service uses REDIS list values to store the UUIDs representing the query executed on the SanteDB server. The data
            is stored in database 2 of the REDIS server.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Caching.Redis.RedisQueryPersistenceService, SanteDB.Caching.Redis, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Security Audit Service - (SanteDB.Core.Api)
An implementation of [IDaemonService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDaemonService.htm) which monitors instances of [IIdentityProviderService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IIdentityProviderService.htm)
            and [ISessionIdentityProviderService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ISessionIdentityProviderService.htm) to audit login and logout events in the audit repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.Audit.AuditDaemonService, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## PubSubBroker - (SanteDB.Core.Api)
An implementation of the [IDaemonService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDaemonService.htm) which is responsible for monitoring
            the [IPubSubManagerService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_PubSub_IPubSubManagerService.htm) for new subscription events
### Description
The Pub/Sub broker is the central daemon which is responsible for coordinating outbound notifications based on 
            filters established by subscribers. The broker:

1. Listens to the ```Subscribe``` event on the [IPubSubManagerService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_PubSub_IPubSubManagerService.htm) and creates a callback for the data event
1. Enqueues any new data to the [IDispatcherQueueManagerService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Queue_IDispatcherQueueManagerService.htm) for sending to outbound recipients
1. When a [IDispatcherQueueManagerService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Queue_IDispatcherQueueManagerService.htm) message is enqueued, loads the appropriate [IPubSubDispatcherFactory](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_PubSub_IPubSubDispatcherFactory.htm) and publishes the notification

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.PubSub.Broker.PubSubBroker, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## DependencyServiceManager - (SanteDB.Core.Api)
The core implementation of [IServiceProvider](https://docs.microsoft.com/en-us/dotnet/api/system.iserviceprovider) and [IServiceManager](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IServiceManager.htm) 
            that supports SanteDB's [dependency injection](https://help.santesuite.org/developers/server-plugins/service-definitions#dependency-injection)
            technology.
### Description
The dependency injection service manager is responsible for:

* Maintaining singleton or per-call instances registered in the [ApplicationServiceContextConfigurationSection](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Configuration_ApplicationServiceContextConfigurationSection.htm)
* Determining the dependencies of each service via ```CreateInjected()``` and ensuring they exist and are constructed for injection
* Validating the digital signatures on assembly files which are used by the SanteDB system (see: [Digital Signing Requirements](https://help.santesuite.org/developers/server-plugins/digital-signing-requirements))
* Calling any [IServiceFactory](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IServiceFactory.htm) instance to attempt to construct missing services
* Coordinating the lifecycle of [IDaemonService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDaemonService.htm) instances


Note: You must have an [IConfigurationManager](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IConfigurationManager.htm) instance registered in the application service context prior to calling the ```Start()``` method on this class

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.DependencyServiceManager, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Default Job Manager - (SanteDB.Core.Api)
SanteDB's default implementation of the [IJobManagerService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Jobs_IJobManagerService.htm)
### Description


### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Jobs.DefaultJobManagerService, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SimDataManagementService - (SanteDB.Core.Api)
Represents a [IDataManagementPattern](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_IDataManagementPattern.htm) which uses destructive merge and matching in order
            to contain a single instance.
### Description
The SIM data management service implements the [Single Instance Mode](https://help.santesuite.org/santedb/data-storage-patterns#single-instance-mode) of
            storage pattern. The single instance mode:

* Maintains a single copy of a record in the CDR
* Attempts to perform duplicate detection between these single instances
* When a merge occurs, the subsumed record is obsoleted (and later purged)
* Unmerge is not possible

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Data.SimDataManagementService, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## DataQualityService - (SanteDB.Core.Api)
A [IDaemonService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDaemonService.htm) which registers [DataQualityBusinessRule`1](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_DataQualityBusinessRule_1.htm) against
            configured targets

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Data.Quality.DataQualityService, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AppletSubscriptionRepository - (SanteDB.Core.Applets)
An implementation of the [ISubscriptionRepository](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ISubscriptionRepository.htm) that loads definitions from applets

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Applets.Services.Impl.AppletSubscriptionRepository, SanteDB.Core.Applets, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AgsService - (SanteDB.DisconnectedClient.Ags)
The Applet Gateway Service
### Description
The AGS service is responsible for starting the REST based services for the dCDR instance and is responsible
            for maintaining and managing these services through the life cycle including:

* [Health Data Service Interface](https://help.santesuite.org/developers/service-apis/health-data-service-interface-hdsi)
* [Administration Management Interface](https://help.santesuite.org/developers/service-apis/administration-management-interface-ami)
* [Business Intelligence Service](https://help.santesuite.org/developers/service-apis/business-intelligence-services-bis)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.DisconnectedClient.Ags.AgsService, SanteDB.DisconnectedClient.Ags, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## BluetoothPeerToPeerShareService - (SanteDB.DisconnectedClient.UI)
An implementation of the [IPeerToPeerShareService](http://santesuite.org/assets/doc/net/html/T_SanteDB_DisconnectedClient_Services_IPeerToPeerShareService.htm) which sends and receives data over bluetooth
### Description
The bluetooth peer to peer sharing service allows SanteDB plug-ins to request and receive ad-hoc data
            between peers using bluetooth file sharing

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.DisconnectedClient.UI.Services.Bluetooth.BluetoothPeerToPeerShareService, SanteDB.DisconnectedClient.UI, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Administrative Management Interface - (SanteDB.Messaging.AMI)
An implementation of the [IApiEndpointProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Interop_IApiEndpointProvider.htm) which hosts and manages the 
            [Administrative Management Interface](https://help.santesuite.org/developers/service-apis/administration-management-interface-ami) REST services.
### Description
This service is responsible for starting up and shutting down the REST services for the AMI, as well as

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Messaging.AMI.AmiMessageHandler, SanteDB.Messaging.AMI, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## FhirDataInitializationService - (SanteDB.Messaging.FHIR)
Scans the configured directory on application startup to import or seed data into SanteDB from FHIR
### Description
This service, like the [DataInitializationService](#DataInitializationService) reads FHIR resource
            files in the configured directory and imports the data from those files (on system startup) into the CDR instance. FHIR resource files
            can be either ```.xml``` or ```.json``` instances.

After data is processed the import process will rename the input file as ```.complete``` and will emit an equivalent file
            suffixed with ```-response``` to indicate any information returned by the FHIR handler for the contained resources.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Messaging.FHIR.FhirDataInitializationService, SanteDB.Messaging.FHIR, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## HL7 FHIR R4 API Endpoint - (SanteDB.Messaging.FHIR)
Implementation of an [IApiEndpointProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Interop_IApiEndpointProvider.htm) for HL7 Fast Health Interoperability Resources (FHIR) REST Interface
### Description
The FHIR based message handler is responsible for starting the [IFhirServiceContract](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_FHIR_Rest_IFhirServiceContract.htm) REST service and 
            enables SanteDB's [FHIR REST](https://help.santesuite.org/developers/service-apis/hl7-fhir) services. Consult the
            [org/developers/service-apis/hl7-fhir/enabling-fhir-interfaces](#org/developers/service-apis/hl7-fhir/enabling-fhir-interfaces) documentation
            for more information on enabling these services in SanteDB.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Messaging.FHIR.FhirMessageHandler, SanteDB.Messaging.FHIR, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GS1 Stock Event Subscriber - (SanteDB.Messaging.GS1)
Represents a notification service that listens to stock events and then prepares them for broadcast
### Description
This service is obsolete and will be replaced using the [PubSubBroker](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_PubSub_Broker_PubSubBroker.htm) implementation and 
            [IPubSubDispatcherFactory](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_PubSub_IPubSubDispatcherFactory.htm) implementation instead.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Messaging.GS1.StockSubscriber, SanteDB.Messaging.GS1, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GS1 BMS XML3.3 API Endpoint - (SanteDB.Messaging.GS1)
GS1 Business Messaging Standard (BMS) HTTP / REST implementation of [IApiEndpointProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Interop_IApiEndpointProvider.htm)
### Description
This service is responsible for maintaining the lifecycle of the [IStockService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_GS1_Rest_IStockService.htm) REST contract
            which implements SanteDB's [GS1 BMS API](https://help.santesuite.org/developers/service-apis/gs1-bms-xml).

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Messaging.GS1.StockServiceMessageHandler, SanteDB.Messaging.GS1, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## GS1 AS2(ish) Integration Service - (SanteDB.Messaging.GS1)
GS1 AS.2 stock event notification service
### Description
This class is obsolete and will be migrated to the [IPubSubDispatcherFactory](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_PubSub_IPubSubDispatcherFactory.htm) implementations in future versions of SanteDB.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Messaging.GS1.Transport.AS2.As2IntegrationService, SanteDB.Messaging.GS1, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Health Data Services Interface - (SanteDB.Messaging.HDSI)
Implementation of [IApiEndpointProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Interop_IApiEndpointProvider.htm) for the Health Data Services Interface REST service
### Description
The HDSI message handler is responsible for the maintenance and lifecycle of SanteDB's 
            [Health Data Service Interface](https://help.santesuite.org/developers/service-apis/health-data-service-interface-hdsi). The service
            starts the necessary REST and query services on start and tears them down on system shutdown.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Messaging.HDSI.HdsiMessageHandler, SanteDB.Messaging.HDSI, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## HL7v2 API Endpoint - (SanteDB.Messaging.HL7)
Implementation of the [IApiEndpointProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Interop_IApiEndpointProvider.htm) providing support for Health Level 7 Version 2.x messaging
### Description
This service is responsible for starting up and tearing down the various [IHL7MessageHandler](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_HL7_IHL7MessageHandler.htm) interfaces
            configured for SanteDB's implementation of [HL7v2 support](https://help.santesuite.org/developers/service-apis/hl7v2). This
            service starts up the necessary [ITransportProtocol](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_HL7_TransportProtocol_ITransportProtocol.htm) interfaces and initializes the message handlers for receiving and handling 
            inbound messages on LLP, SLLP, or TCP.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Messaging.HL7.HL7MessageHandler, SanteDB.Messaging.HL7, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## OpenAPI Metadata Exchange - (SanteDB.Messaging.Metadata)
Represents the daemon service that starts/stops the OpenApi information file

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Messaging.Metadata.MetadataMessageHandler, SanteDB.Messaging.Metadata, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ADO.NET Data Persistence Service - (SanteDB.Persistence.Data.ADO)
Registers and configures the necessary sub-services and [IDataPersistenceService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataPersistenceService.htm) implementations
            to allow SanteDB iCDR to persist, query, and read messages from available ADO.NET data providers
### Description
This service is responsible for registering the necessary [IDataPersistenceService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataPersistenceService.htm) providers
            which are responsible for interfacing the SanteDB [Physical Model](https://help.santesuite.org/santedb/data-and-information-architecture/physical-model) 
            with the SanteDB [Business / Object Model](https://help.santesuite.org/santedb/data-and-information-architecture/conceptual-data-model). Each 
            persistence implementation is derived from the [ModelMap](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Map_ModelMap.htm) configuration, and is uses the ADO.NET classes to via the [IDbProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_OrmLite_Providers_IDbProvider.htm) configured.

Additionally, on start of the SanteDB iCDR or dCDR, this service is responsible for applying any [Data Patches](https://help.santesuite.org/developers/server-plugins/database-patching)
            which have been provided (compiled via an embedded resource) by any of the validated SanteDB plugins.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MDM Data Repository - (SanteDB.Persistence.MDM)
An implementation of the [IDataManagementPattern](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_IDataManagementPattern.htm) which keeps multiple copies of 
            source records and maintains linkages with a single master record.
### Description
The MDM data management service provides the [Master Data Storage](https://help.santesuite.org/santedb/data-storage-patterns/master-data-storage) pattern
            for SanteDB. This service is responsible for creating subscribers to listen to events from the [IRepositoryService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRepositoryService.htm) layer in SanteDB
            and take appropriate actions to seggregate source information form record of truth information. Additionally, this service registers implementations
            of [IFreetextSearchService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IFreetextSearchService.htm), [IRecordMatchingService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Matching_IRecordMatchingService.htm), [IRecordMergingService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRecordMergingService.htm) and [ISubscriptionExecutor](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ISubscriptionExecutor.htm) functionality to ensure the freetext and subscription requests are 
            properly handled and synthesized.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.MDM.Services.MdmDataManagementService, SanteDB.Persistence.MDM, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Business Intelligence Service - (SanteDB.Rest.BIS)
Represents a message handler for the BIS

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Rest.BIS.BisMessageHandler, SanteDB.Rest.BIS, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Local (database) repository service - (SanteDB.Server.Core)
Registers the [IRepositoryService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRepositoryService.htm) instances with the core application context and provides a 
            [IServiceFactory](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IServiceFactory.htm) implementation to construct repository services.
### Description
The instances of [IRepositoryService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRepositoryService.htm) which this service constructs contact directly with the 
            equivalent [IDataPersistenceService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataPersistenceService.htm) for each object. The repository layers add business process
            logic for calling [IBusinessRulesService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IBusinessRulesService.htm), [IPrivacyEnforcementService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_IPrivacyEnforcementService.htm), and others as 
            necessary to ensure secure and safe access to the underlying data repositories. All requests to any [IRepositoryService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRepositoryService.htm)
            constructed by this service use the [AuthenticationContext](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_AuthenticationContext.htm) to establish "who" is performing the action.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalRepositoryService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Local Applet Repository/Manager - (SanteDB.Server.Core)
Represents an applet manager service that uses the local file system

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalAppletManagerService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Applet JavaScript BRE - (SanteDB.Server.Core)
A daemon which loads business rules from the applet manager

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Daemons.AppletBusinessRulesDaemon, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Dataset Installation Service - (SanteDB.Server.Core)
Data initialization service
### Description
This service reads data from the configured directory (usually the ```data/``` directory) with extension ```.dataset```
            and imports the data into the SanteDB iCDR instance. Each [Dataset](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Export_Dataset.htm) file is then renamed to ```.completed``` to 
            indicate that the import of the provided data was successful. This service allows SanteDB instances to share information between
            deployments easily.

For more information consult the [Distributing Data](https://help.santesuite.org/developers/applets/distributing-data) files

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Persistence.DataInitializationService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Debugger: Data Sandbox UI - (SanteDB.Tools.Debug)
TODO: Document this

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Tools.Debug.DataSandboxService, SanteDB.Tools.Debug, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## File Based BI Repository - (SanteDB.Tools.Debug)
TODO: Document this

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Tools.Debug.BI.FileMetadataRepository, SanteDB.Tools.Debug, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyDaemonService : SanteDB.Core.Services.IDaemonService { 
	public String ServiceName => "My own IDaemonService service";
	/// <summary>
	/// Fired when the daemon service has commenced start but has not yet finished
	/// </summary>
	public event EventHandler Starting;
	/// <summary>
	/// Fired when the daemon service has completed it start procedure.
	/// </summary>
	public event EventHandler Started;
	/// <summary>
	/// Fired when the daemon service has commenced stop but has not yet been fully shut down.
	/// </summary>
	public event EventHandler Stopping;
	/// <summary>
	/// Fired when the daemon has completed its stop procedure
	/// </summary>
	public event EventHandler Stopped;
	/// <summary>
	/// Indicates whether the daemon service is running
	/// </summary>
	public Boolean IsRunning {
		get;
	}
	public Boolean Start(){
		throw new System.NotImplementedException();
	}
	public Boolean Stop(){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDaemonService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDaemonService.htm)
* [OAuthMessageHandler C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Authentication_OAuth2_OAuthMessageHandler.htm)
* [MemoryCacheService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Memory_MemoryCacheService.htm)
* [RedisAdhocCache C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Redis_RedisAdhocCache.htm)
* [RedisCacheService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Redis_RedisCacheService.htm)
* [RedisQueryPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Redis_RedisQueryPersistenceService.htm)
* [AuditDaemonService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Audit_AuditDaemonService.htm)
* [Publish Subscribe Broker C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_PubSub_Broker_PubSubBroker.htm)
* [DependencyServiceManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_DependencyServiceManager.htm)
* [DefaultJobManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Jobs_DefaultJobManagerService.htm)
* [SimDataManagementService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_SimDataManagementService.htm)
* [DataQualityService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_DataQualityService.htm)
* [AppletSubscriptionRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Applets_Services_Impl_AppletSubscriptionRepository.htm)
* [AgsService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_DisconnectedClient_Ags_AgsService.htm)
* [BluetoothPeerToPeerShareService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_DisconnectedClient_UI_Services_Bluetooth_BluetoothPeerToPeerShareService.htm)
* [The AMI provides administrative operations for SanteDB over HTTP C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_AMI_AmiMessageHandler.htm)
* [FhirDataInitializationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_FHIR_FhirDataInitializationService.htm)
* [Allows SanteDB iCDR to send and receive HL7 FHIR R4 messages C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_FHIR_FhirMessageHandler.htm)
* [StockSubscriber C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_GS1_StockSubscriber.htm)
* [Allows SanteDB iCDR to send and receive GS1 BMS XML messages over REST based transport C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_GS1_StockServiceMessageHandler.htm)
* [As2IntegrationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_GS1_Transport_AS2_As2IntegrationService.htm)
* [The primary iCDR Health Data Messaging Service (HDSI) allows sharing of RIM objects in XML or JSON over HTTP C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_HDSI_HdsiMessageHandler.htm)
* [HL7MessageHandler C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_HL7_HL7MessageHandler.htm)
* [Allows SanteDB iCDR/dCDR to expose service metadata using OpenAPI/Swagger 2.0 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_Metadata_MetadataMessageHandler.htm)
* [AdoPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoPersistenceService.htm)
* [MdmDataManagementService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_MDM_Services_MdmDataManagementService.htm)
* [Exposes the SanteDB Business Intelligence functions (reports, queries, etc.) over HTTP REST C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Rest_BIS_BisMessageHandler.htm)
* [LocalRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalRepositoryService.htm)
* [LocalAppletManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalAppletManagerService.htm)
* [AppletBusinessRulesDaemon C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Daemons_AppletBusinessRulesDaemon.htm)
* [DataInitializationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Persistence_DataInitializationService.htm)
* [DataSandboxService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Tools_Debug_DataSandboxService.htm)
* [FileMetadataRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Tools_Debug_BI_FileMetadataRepository.htm)

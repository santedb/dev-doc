`IDaemonService` in assembly SanteDB.Core.Api version 3.0.1980.0

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


## Applet JavaScript BRE - (SanteDB.BusinessRules.JavaScript)
A daemon which loads business rules from the applet manager

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.BusinessRules.JavaScript.AppletBusinessRulesDaemon, SanteDB.BusinessRules.JavaScript, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Caching.Memory.MemoryCacheService, SanteDB.Caching.Memory, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Caching.Redis.RedisAdhocCache, SanteDB.Caching.Redis, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Caching.Redis.RedisCacheService, SanteDB.Caching.Redis, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Caching.Redis.RedisQueryPersistenceService, SanteDB.Caching.Redis, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## UpstreamSynchronizationService - (SanteDB.Client.Disconnected)
An implementation of the [ISynchronizationService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Disconnected_Data_Synchronization_ISynchronizationService.htm) which pulls HDSI and AMI data from the remote

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Disconnected.Data.Synchronization.UpstreamSynchronizationService, SanteDB.Client.Disconnected, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Security Audit Service - (SanteDB.Core.Api)
An implementation of [IDaemonService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDaemonService.htm) which monitors instances of [IIdentityProviderService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IIdentityProviderService.htm)
            and [ISessionIdentityProviderService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_ISessionIdentityProviderService.htm) to audit login and logout events in the audit repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.Audit.AuditDaemonService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Core.PubSub.Broker.PubSubBroker, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Core.Services.Impl.DependencyServiceManager, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ServerMonitorService - (SanteDB.Core.Api)
Represents a security monitoring service which notifies the administrator based on a series of events

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Management.ServerMonitorService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Core.Jobs.DefaultJobManagerService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Core.Data.Quality.DataQualityService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Core.Data.Management.SimDataManagementService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Dataset Installation Service - (SanteDB.Core.Api)
Data initialization service
### Description
This service will read all datasets provided by any registered [IDatasetProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Initialization_IDatasetProvider.htm) and will instal them via the 
            configured [IDatasetInstallerService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Initialization_IDatasetInstallerService.htm)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Data.Initialization.DataInitializationService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AppletNotificationTemplateRepository - (SanteDB.Core.Applets)
An implementation of the [INotificationTemplateRepository](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Notifications_INotificationTemplateRepository.htm) which loads [NotificationTemplate](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Notifications_NotificationTemplate.htm) instances
            from the ```notification/``` folder in applets

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Applets.Services.Impl.AppletNotificationTemplateRepository, SanteDB.Core.Applets, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Core.Applets.Services.Impl.AppletSubscriptionRepository, SanteDB.Core.Applets, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Local Applet Repository/Manager - (SanteDB.Core.Applets)
Represents an applet manager service that uses the local file system

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Applets.Services.Impl.FileSystemAppletManagerService, SanteDB.Core.Applets, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## HL7 FHIR R4 API Endpoint - (SanteDB.Messaging.FHIR)
Implementation of an [IApiEndpointProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Interop_IApiEndpointProvider.htm) for HL7 Fast Health Interoperability Resources (FHIR) REST Interface
### Description
The FHIR based message handler is responsible for starting the [IFhirServiceContract](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_FHIR_Rest_IFhirServiceContract.htm) REST service and 
            enables SanteDB's [FHIR REST](https://help.santesuite.org/developers/service-apis/hl7-fhir) services. Consult the
            [Enabling FHIR Interfaces](https://help.santesuite.org/developers/service-apis/hl7-fhir/enabling-fhir-interfaces) documentation
            for more information on enabling these services in SanteDB.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Messaging.FHIR.FhirMessageHandler, SanteDB.Messaging.FHIR, Version=3.0.1982.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Messaging.GS1.StockServiceMessageHandler, SanteDB.Messaging.GS1, Version=3.0.1982.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Messaging.GS1.StockSubscriber, SanteDB.Messaging.GS1, Version=3.0.1982.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Messaging.GS1.Transport.AS2.As2IntegrationService, SanteDB.Messaging.GS1, Version=3.0.1982.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Messaging.HL7.HL7MessageHandler, SanteDB.Messaging.HL7, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Messaging.Metadata.MetadataMessageHandler, SanteDB.Messaging.Metadata, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Administrative Management Interface - (SanteDB.Rest.AMI)
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
		<add type="SanteDB.Rest.AMI.AmiMessageHandler, SanteDB.Rest.AMI, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Application Interaction Interface - (SanteDB.Rest.AppService)
Implementation of [IApiEndpointProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Interop_IApiEndpointProvider.htm) for the Application Service REST service
### Description
The application service manager is used for end-user facing CDR deployments and provides methods for manipulating 
            the user environment

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Rest.AppService.AppServiceMessageHandler, SanteDB.Rest.AppService, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Rest.BIS.BisMessageHandler, SanteDB.Rest.BIS, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Health Data Services Interface - (SanteDB.Rest.HDSI)
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
		<add type="SanteDB.Rest.HDSI.HdsiMessageHandler, SanteDB.Rest.HDSI, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## OAuth 2.0 Messaging Provider - (SanteDB.Rest.OAuth)
Represents a [IApiEndpointProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Interop_IApiEndpointProvider.htm) which serves OpenID Connect and 
            OAUTH requests
### Description
This service is responsible for starting and maintaining the [OAuthServiceBehavior](http://santesuite.org/assets/doc/net/html/T_SanteDB_Rest_OAuth_Rest_OAuthServiceBehavior.htm) REST service which 
            is responsible for supporting SanteDB's [OpenID Connect](https://help.santesuite.org/developers/service-apis/openid-connect) interface

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Rest.OAuth.OAuthMessageHandler, SanteDB.Rest.OAuth, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## WWW Interface - (SanteDB.Rest.WWW)
Implementation of [IApiEndpointProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Interop_IApiEndpointProvider.htm) for the World Wide Web service
### Description
The world wide web message handler is responsible for serving HTTP requests for web pages

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Rest.WWW.WwwMessageHandler, SanteDB.Rest.WWW, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
* [AppletBusinessRulesDaemon C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_BusinessRules_JavaScript_AppletBusinessRulesDaemon.htm)
* [MemoryCacheService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Memory_MemoryCacheService.htm)
* [RedisAdhocCache C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Redis_RedisAdhocCache.htm)
* [RedisCacheService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Redis_RedisCacheService.htm)
* [RedisQueryPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Redis_RedisQueryPersistenceService.htm)
* [UpstreamSynchronizationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Disconnected_Data_Synchronization_UpstreamSynchronizationService.htm)
* [AuditDaemonService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Audit_AuditDaemonService.htm)
* [Publish Subscribe Broker C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_PubSub_Broker_PubSubBroker.htm)
* [DependencyServiceManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_DependencyServiceManager.htm)
* [ServerMonitorService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Management_ServerMonitorService.htm)
* [DefaultJobManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Jobs_DefaultJobManagerService.htm)
* [DataQualityService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_DataQualityService.htm)
* [SimDataManagementService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Management_SimDataManagementService.htm)
* [DataInitializationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Initialization_DataInitializationService.htm)
* [AppletNotificationTemplateRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Applets_Services_Impl_AppletNotificationTemplateRepository.htm)
* [AppletSubscriptionRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Applets_Services_Impl_AppletSubscriptionRepository.htm)
* [FileSystemAppletManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Applets_Services_Impl_FileSystemAppletManagerService.htm)
* [Allows SanteDB iCDR to send and receive HL7 FHIR R4 messages C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_FHIR_FhirMessageHandler.htm)
* [Allows SanteDB iCDR to send and receive GS1 BMS XML messages over REST based transport C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_GS1_StockServiceMessageHandler.htm)
* [StockSubscriber C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_GS1_StockSubscriber.htm)
* [As2IntegrationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_GS1_Transport_AS2_As2IntegrationService.htm)
* [HL7MessageHandler C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_HL7_HL7MessageHandler.htm)
* [Allows SanteDB iCDR/dCDR to expose service metadata using OpenAPI/Swagger 2.0 C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Messaging_Metadata_MetadataMessageHandler.htm)
* [The AMI provides administrative operations for SanteDB over HTTP C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Rest_AMI_AmiMessageHandler.htm)
* [Application Service C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Rest_AppService_AppServiceMessageHandler.htm)
* [Exposes the SanteDB Business Intelligence functions (reports, queries, etc.) over HTTP REST C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Rest_BIS_BisMessageHandler.htm)
* [The primary iCDR Health Data Messaging Service (HDSI) allows sharing of RIM objects in XML or JSON over HTTP C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Rest_HDSI_HdsiMessageHandler.htm)
* [OAuthMessageHandler C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Rest_OAuth_OAuthMessageHandler.htm)
* [WwwMessageHandler C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Rest_WWW_WwwMessageHandler.htm)

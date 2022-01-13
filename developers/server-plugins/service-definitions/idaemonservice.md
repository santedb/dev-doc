---
description: IDaemonService (IDaemonService in SanteDB.Core.Api)
---

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
|Start|Boolean||TODO|
|Stop|Boolean||TODO|

# Implementations


## OAuth 2.0 Token Service - (SanteDB.Authentication.OAuth2)
OAuth2 message handler

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

## SECURITY AUDIT SERVICE - (SanteDB.Core.Api)
A daemon service which listens to audit sources and forwards them to the auditor

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
A pub-sub broker which is responsible for actually facilitating the publish/subscribe
            logic

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
Represents a service manager and provider that supports DI
### Description
You must have an IConfigurationManager instance registered in order to use this service

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
Represents the default implementation of the timer

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
Represents a daemon service that registers a series of merge services which can merge records together

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
The data quality service handler

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
An implementation of the ISubscriptionRepository that loads definitions from applets

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

## Administrative Messaging Interface - (SanteDB.Messaging.AMI)
AMI Message handler

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
FHIR based data initialization service

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
Message handler for FHIR

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

## StockSubscriber - (SanteDB.Messaging.GS1)
Represents a notification service that listens to stock events and then prepares them for broadcast

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
Stock service message handler

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
GS1 Stock Integration Service

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
The HDSI Message Handler Daemon class

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
Message handler service

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
Represents a dummy service which just adds the persistence services to the context

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

## MIDM Data Repository - (SanteDB.Persistence.MDM)
The MdmRecordDaemon is responsible for subscribing to MDM targets in the configuration
            and linking/creating master records whenever a record of that type is created.

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
Daemon service which adds all the repositories for acts

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
* [PubSubBroker C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_PubSub_Broker_PubSubBroker.htm)
* [DependencyServiceManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_DependencyServiceManager.htm)
* [DefaultJobManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Jobs_DefaultJobManagerService.htm)
* [SimDataManagementService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_SimDataManagementService.htm)
* [DataQualityService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_DataQualityService.htm)
* [AppletSubscriptionRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Applets_Services_Impl_AppletSubscriptionRepository.htm)
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

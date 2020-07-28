---
description: IDaemonService (SanteDB.Core.Api)
---

# Daemon Services

## Summary

Daemon service which runs when the application is started

## Events

| Event | Type | Description |
| :--- | :--- | :--- |
| Starting | EventHandler | Fired when the daemon is starting |
| Started | EventHandler | Fired when the daemon is started |
| Stopping | EventHandler | Fired when the daemon is stopping |
| Stopped | EventHandler | Fired when the daemon has stopped |

## Properties

| Property | Type | Access | Description |
| :--- | :--- | :--- | :--- |
| IsRunning | Boolean | R | True when daemon is running |

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| Start | Boolean |  | TODO |
| Stop | Boolean |  | TODO |

## Implementations

### OAuth 2.0 Token Service - \(SanteDB.Authentication.OAuth2\)

OAuth2 message handler

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Authentication.OAuth2.OAuthMessageHandler, SanteDB.Authentication.OAuth2, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### Memory Cache Service - \(SanteDB.Caching.Memory\)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Caching.Memory.MemoryCacheService, SanteDB.Caching.Memory, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### Memory-Based Query Persistence Service - \(SanteDB.Caching.Memory\)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Caching.Memory.MemoryQueryPersistenceService, SanteDB.Caching.Memory, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### RedisAdhocCache - \(SanteDB.Caching.Redis\)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Caching.Redis.RedisAdhocCache, SanteDB.Caching.Redis, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### REDIS Data Caching Service - \(SanteDB.Caching.Redis\)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Caching.Redis.RedisCacheService, SanteDB.Caching.Redis, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### REDIS Query Persistence Service - \(SanteDB.Caching.Redis\)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Caching.Redis.RedisQueryPersistenceService, SanteDB.Caching.Redis, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### Default Policy Enforcement Service - \(SanteDB.Core.Api\)

Local policy enforcement point service

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Security.Privacy.DataPolicyFilterService, SanteDB.Core.Api, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### SECURITY AUDIT SERVICE - \(SanteDB.Core.Api\)

A daemon service which listens to audit sources and forwards them to the auditor

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Security.Audit.AuditDaemonService, SanteDB.Core.Api, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### SimDataManagementService - \(SanteDB.Core.Api\)

Represents a daemon service that registers a series of merge services which can merge records together

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Data.SimDataManagementService, SanteDB.Core.Api, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### DataQualityService - \(SanteDB.Core.Api\)

The data quality service handler

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Data.Quality.DataQualityService, SanteDB.Core.Api, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### AppletSubscriptionRepository - \(SanteDB.Core.Applets\)

An implementation of the ISubscriptionRepository that loads definitions from applets

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Applets.Services.Impl.AppletSubscriptionRepository, SanteDB.Core.Applets, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### Default Job Manager - \(SanteDB.Core\)

Represents the default implementation of the timer

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Services.DefaultJobManagerService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### Local \(database\) repository service - \(SanteDB.Core\)

Daemon service which adds all the repositories for acts

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Services.Impl.LocalRepositoryService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### Local Applet Repository/Manager - \(SanteDB.Core\)

Represents an applet manager service that uses the local file system

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Services.Impl.LocalAppletManagerService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### Applet JavaScript BRE - \(SanteDB.Core\)

A daemon which loads business rules from the applet manager

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Services.Daemons.AppletBusinessRulesDaemon, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### ExemptablePolicyFilterService - \(SanteDB.Core\)

Local policy enforcement point service

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Security.Privacy.ExemptablePolicyFilterService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### Dataset Installation Service - \(SanteDB.Core\)

Data initialization service

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Persistence.DataInitializationService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### Administrative REST Daemon - \(SanteDB.Messaging.AMI\)

AMI Message handler

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Messaging.AMI.AmiMessageHandler, SanteDB.Messaging.AMI, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### HL7 FHIR R3 API Endpoint - \(SanteDB.Messaging.FHIR\)

Message handler for FHIR

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Messaging.FHIR.FhirMessageHandler, SanteDB.Messaging.FHIR, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### GS1 Stock Event Subscriber - \(SanteDB.Messaging.GS1\)

Represents a notification service that listens to stock events and then prepares them for broadcast

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Messaging.GS1.StockSubscriber, SanteDB.Messaging.GS1, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### GS1 BMS XML3.3 API Endpoint - \(SanteDB.Messaging.GS1\)

Stock service message handler

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Messaging.GS1.StockServiceMessageHandler, SanteDB.Messaging.GS1, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### GS1 AS2\(ish\) Integration Service - \(SanteDB.Messaging.GS1\)

GS1 Stock Integration Service

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Messaging.GS1.Transport.AS2.As2IntegrationService, SanteDB.Messaging.GS1, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### iCDR Message Service - \(SanteDB.Messaging.HDSI\)

The HDSI Message Handler Daemon class

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Messaging.HDSI.HdsiMessageHandler, SanteDB.Messaging.HDSI, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### HL7v2 API Endpoint - \(SanteDB.Messaging.HL7\)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Messaging.HL7.HL7MessageHandler, SanteDB.Messaging.HL7, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### OpenAPI Metadata Exchange - \(SanteDB.Messaging.Metadata\)

Represents the daemon service that starts/stops the OpenApi information file

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Messaging.Metadata.MetadataMessageHandler, SanteDB.Messaging.Metadata, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### RISI API Daemon - \(SanteDB.Messaging.RISI\)

Represents a message handler for reporting services.

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Messaging.RISI.RisiMessageHandler, SanteDB.Messaging.RISI, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### ADO.NET Data Persistence Service - \(SanteDB.Persistence.Data.ADO\)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Persistence.Data.ADO.Services.AdoPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### MIDM Data Repository - \(SanteDB.Persistence.MDM\)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Persistence.MDM.Services.MdmDataManagementService, SanteDB.Persistence.MDM, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### ADO.NET Report/Wareouse Persistence - \(SanteDB.Persistence.Reporting.ADO\)

Represents a persistence service for reporting services.

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Persistence.Reporting.ADO.ReportingPersistenceService, SanteDB.Persistence.Reporting.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### BIS REST Daemon - \(SanteDB.Rest.BIS\)

Represents a message handler for the BIS

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Rest.BIS.BisMessageHandler, SanteDB.Rest.BIS, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### Debugger: Data Sandbox UI - \(SanteDB.Tools.DataSandbox\)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Tools.DataSandbox.DataSandboxService, SanteDB.Tools.DataSandbox, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### File Based BI Repository - \(SanteDB.Tools.Debug\)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Tools.Debug.BI.FileMetadataRepository, SanteDB.Tools.Debug, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyDaemonService : SanteDB.Core.Services.IDaemonService { 
    public String ServiceName => "My own IDaemonService service";
    /// <summary>
    /// Fired when the daemon is starting
    /// </summary>
    public event EventHandler Starting;
    /// <summary>
    /// Fired when the daemon is started
    /// </summary>
    public event EventHandler Started;
    /// <summary>
    /// Fired when the daemon is stopping
    /// </summary>
    public event EventHandler Stopping;
    /// <summary>
    /// Fired when the daemon has stopped
    /// </summary>
    public event EventHandler Stopped;
    /// <summary>
    /// True when daemon is running
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


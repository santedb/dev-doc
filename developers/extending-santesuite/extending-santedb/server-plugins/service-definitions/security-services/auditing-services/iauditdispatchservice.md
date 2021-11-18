---
description: IAuditDispatchService (SanteDB.Core.Api)
---

# Audit Dispatching Service

## Summary

Represents a service that dispatches audits to a central repository

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| SendAudit | void | _AuditData_ **audit** | Sends the audit to the central authority |

## Implementations

### IHE ATNA Audit Dispatcher - \(SanteDB.Messaging.Atna\)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Messaging.Atna.AtnaAuditService, SanteDB.Messaging.Atna, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyAuditDispatchService : SanteDB.Core.Services.IAuditDispatchService { 
    public String ServiceName => "My own IAuditDispatchService service";
    /// <summary>
    /// Sends the audit to the central authority
    /// </summary>
    public void SendAudit(AuditData audit){
        throw new System.NotImplementedException();
    }
}
```


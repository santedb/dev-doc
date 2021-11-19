---
description: ISessionProviderService (SanteDB.Core.Api)
---

# Session Manager Service

## Summary

Represents a service which is responsible for the storage and retrieval of sessions

## Events

| Event       | Type                                       | Description                                                              |
| ----------- | ------------------------------------------ | ------------------------------------------------------------------------ |
| Established | EventHandler\<SessionEstablishedEventArgs> | Fired when the session provider service has established                  |
| Abandoned   | EventHandler\<SessionEstablishedEventArgs> | Fired when the session provider service has ended by the user's decision |

## Operations

| Operation | Response/Return | Input/Parameter                                                                                                                                                                                                                                                                     | Description                                                 |
| --------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| Establish | ISession        | <p><em>IPrincipal</em> <strong>principal</strong><br><em>String</em> <strong>remoteEp</strong><br><em>Boolean</em> <strong>isOverride</strong><br><em>String</em> <strong>purpose</strong><br><em>String[]</em> <strong>scope</strong><br><em>String</em> <strong>lang</strong></p> | Establishes a session for the specified principal           |
| Get       | ISession        | <p><em>Byte[]</em> <strong>sessionToken</strong><br><em>Boolean</em> <strong>allowExpired</strong></p>                                                                                                                                                                              | Authenticates the session identifier as evidence of session |
| Extend    | ISession        | _Byte\[]_ **refreshToken**                                                                                                                                                                                                                                                          | Extend the session with the specified refresh token         |
| Abandon   | void            | _ISession_ **session**                                                                                                                                                                                                                                                              | Abandons the session                                        |

## Implementations

### ADO.NET Session Storage - (SanteDB.Persistence.Data.ADO)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Persistence.Data.ADO.Services.AdoSessionProvider, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MySessionProviderService : SanteDB.Core.Services.ISessionProviderService { 
    public String ServiceName => "My own ISessionProviderService service";
    /// <summary>
    /// Fired when the session provider service has established
    /// </summary>
    public event EventHandler<SessionEstablishedEventArgs> Established;
    /// <summary>
    /// Fired when the session provider service has ended by the user's decision
    /// </summary>
    public event EventHandler<SessionEstablishedEventArgs> Abandoned;
    /// <summary>
    /// Establishes a session for the specified principal
    /// </summary>
    public ISession Establish(IPrincipal principal,String remoteEp,Boolean isOverride,String purpose,String[] scope,String lang){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Authenticates the session identifier as evidence of session
    /// </summary>
    public ISession Get(Byte[] sessionToken,Boolean allowExpired){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Extend the session with the specified refresh token
    /// </summary>
    public ISession Extend(Byte[] refreshToken){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Abandons the session
    /// </summary>
    public void Abandon(ISession session){
        throw new System.NotImplementedException();
    }
}
```

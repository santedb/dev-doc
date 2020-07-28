---
description: IApplicationIdentityProviderService (SanteDB.Core.Api)
---

# Application Identity Provider

## Summary

Represents a service which retrieves IPrincipal objects for applications.

## Events

| Event | Type | Description |
| :--- | :--- | :--- |
| Authenticated | EventHandler&lt;AuthenticatedEventArgs&gt; | Fired after an authentication request has been made. |
| Authenticating | EventHandler&lt;AuthenticatingEventArgs&gt; | Fired prior to an authentication request being made. |

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| Authenticate | IPrincipal | _String_ **applicationId** _String_ **applicationSecret** | Authenticate the application identity. |
| GetIdentity | IIdentity | _String_ **name** | Gets the specified identity for an application. |
| SetLockout | void | _String_ **name** _Boolean_ **lockoutState** _IPrincipal_ **principal** | Set the lockout status |
| ChangeSecret | void | _String_ **name** _String_ **secret** _IPrincipal_ **principal** | Change the specified application identity's secret |

## Implementations

### ADO.NET Application Identity Provider - \(SanteDB.Persistence.Data.ADO\)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Persistence.Data.ADO.Services.AdoApplicationIdentityProvider, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyApplicationIdentityProviderService : SanteDB.Core.Security.Services.IApplicationIdentityProviderService { 
    public String ServiceName => "My own IApplicationIdentityProviderService service";
    /// <summary>
    /// Fired after an authentication request has been made.
    /// </summary>
    public event EventHandler<AuthenticatedEventArgs> Authenticated;
    /// <summary>
    /// Fired prior to an authentication request being made.
    /// </summary>
    public event EventHandler<AuthenticatingEventArgs> Authenticating;
    /// <summary>
    /// Authenticate the application identity.
    /// </summary>
    public IPrincipal Authenticate(String applicationId,String applicationSecret){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Gets the specified identity for an application.
    /// </summary>
    public IIdentity GetIdentity(String name){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Set the lockout status
    /// </summary>
    public void SetLockout(String name,Boolean lockoutState,IPrincipal principal){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Change the specified application identity's secret
    /// </summary>
    public void ChangeSecret(String name,String secret,IPrincipal principal){
        throw new System.NotImplementedException();
    }
}
```


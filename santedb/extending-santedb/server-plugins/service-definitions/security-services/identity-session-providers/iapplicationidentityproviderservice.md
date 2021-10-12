---
description: IApplicationIdentityProviderService (SanteDB.Core.Api)
---

# Application Identity Provider

## Summary

Represents a service which retrieves IPrincipal objects for applications.

## Events

| Event          | Type                                   | Description                                          |
| -------------- | -------------------------------------- | ---------------------------------------------------- |
| Authenticated  | EventHandler\<AuthenticatedEventArgs>  | Fired after an authentication request has been made. |
| Authenticating | EventHandler\<AuthenticatingEventArgs> | Fired prior to an authentication request being made. |

## Operations

| Operation    | Response/Return | Input/Parameter                                                                                                                                  | Description                                        |
| ------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------- |
| Authenticate | IPrincipal      | <p><em>String</em> <strong>applicationId</strong><br><em>String</em> <strong>applicationSecret</strong></p>                                      | Authenticate the application identity.             |
| GetIdentity  | IIdentity       | _String_ **name**                                                                                                                                | Gets the specified identity for an application.    |
| SetLockout   | void            | <p><em>String</em> <strong>name</strong><br><em>Boolean</em> <strong>lockoutState</strong><br><em>IPrincipal</em> <strong>principal</strong></p> | Set the lockout status                             |
| ChangeSecret | void            | <p><em>String</em> <strong>name</strong><br><em>String</em> <strong>secret</strong><br><em>IPrincipal</em> <strong>principal</strong></p>        | Change the specified application identity's secret |

## Implementations

### ADO.NET Application Identity Provider - (SanteDB.Persistence.Data.ADO)

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

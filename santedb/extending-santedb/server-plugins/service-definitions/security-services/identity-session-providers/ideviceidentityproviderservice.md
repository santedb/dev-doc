---
description: IDeviceIdentityProviderService (SanteDB.Core.Api)
---

# Device Identity Provider

## Summary

Represents an identity service which authenticates devices.

## Events

| Event          | Type                                   | Description                                          |
| -------------- | -------------------------------------- | ---------------------------------------------------- |
| Authenticated  | EventHandler\<AuthenticatedEventArgs>  | Fired after an authentication request has been made. |
| Authenticating | EventHandler\<AuthenticatingEventArgs> | Fired prior to an authentication request being made. |

## Operations

| Operation    | Response/Return | Input/Parameter                                                                                                                                                | Description                                    |
| ------------ | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| Authenticate | IPrincipal      | <p><em>String</em> <strong>deviceId</strong><br><em>String</em> <strong>deviceSecret</strong><br><em>AuthenticationMethod</em> <strong>authMethod</strong></p> | Authenticates the specified device identifier. |
| GetIdentity  | IIdentity       | _String_ **name**                                                                                                                                              | Gets the specified identity for an device.     |
| SetLockout   | void            | <p><em>String</em> <strong>name</strong><br><em>Boolean</em> <strong>lockoutState</strong><br><em>IPrincipal</em> <strong>principal</strong></p>               | Set the lockout status                         |
| ChangeSecret | void            | <p><em>String</em> <strong>name</strong><br><em>String</em> <strong>deviceSecret</strong><br><em>IPrincipal</em> <strong>systemPrincipal</strong></p>          | Change the device secret                       |

## Implementations

### ADO.NET Device Identity Provider - (SanteDB.Persistence.Data.ADO)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Persistence.Data.ADO.Services.AdoDeviceIdentityProvider, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyDeviceIdentityProviderService : SanteDB.Core.Security.Services.IDeviceIdentityProviderService { 
    public String ServiceName => "My own IDeviceIdentityProviderService service";
    /// <summary>
    /// Fired after an authentication request has been made.
    /// </summary>
    public event EventHandler<AuthenticatedEventArgs> Authenticated;
    /// <summary>
    /// Fired prior to an authentication request being made.
    /// </summary>
    public event EventHandler<AuthenticatingEventArgs> Authenticating;
    /// <summary>
    /// Authenticates the specified device identifier.
    /// </summary>
    public IPrincipal Authenticate(String deviceId,String deviceSecret,AuthenticationMethod authMethod){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Gets the specified identity for an device.
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
    /// Change the device secret
    /// </summary>
    public void ChangeSecret(String name,String deviceSecret,IPrincipal systemPrincipal){
        throw new System.NotImplementedException();
    }
}
```

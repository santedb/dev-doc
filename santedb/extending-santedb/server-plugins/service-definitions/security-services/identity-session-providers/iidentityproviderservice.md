---
description: IIdentityProviderService (SanteDB.Core.Api)
---

# User Identity Provider

## Summary

Identity provider service

## Events

| Event | Type | Description |
| :--- | :--- | :--- |
| Authenticating | EventHandler&lt;AuthenticatingEventArgs&gt; | Fired prior to an authentication event |
| Authenticated | EventHandler&lt;AuthenticatedEventArgs&gt; | Fired after an authentication decision being made |

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| GetIdentity | IIdentity | _String_ **userName** | Retrieves an identity from the object |
| GetIdentity | IIdentity | _Guid_ **sid** | Retrieves an identity from the object |
| CreateIdentity | IIdentity | _String_ **userName** _String_ **password** _IPrincipal_ **principal** | Create a basic identity in the provider |
| Authenticate | IPrincipal | _String_ **userName** _String_ **password** | Authenticate the user creating an identity |
| Authenticate | IPrincipal | _String_ **userName** _String_ **password** _String_ **tfaSecret** | Authenticate the user creating an identity |
| ReAuthenticate | IPrincipal | _IPrincipal_ **principal** | Perform a re-authentication of the principal |
| ChangePassword | void | _String_ **userName** _String_ **newPassword** _IPrincipal_ **principal** | Change user password |
| GenerateTfaSecret | String | _String_ **userName** | Set the user's two factor authentication secret |
| DeleteIdentity | void | _String_ **userName** _IPrincipal_ **principal** | Delete an identity |
| SetLockout | void | _String_ **userName** _Boolean_ **lockout** _IPrincipal_ **principal** | Set lockout |
| AddClaim | void | _String_ **userName** _IClaim_ **claim** _IPrincipal_ **principal** _Nullable&lt;TimeSpan&gt;_ **expiriy** | Adds a claim to the specified user account |
| RemoveClaim | void | _String_ **userName** _String_ **claimType** _IPrincipal_ **principal** | Removes a claim from the specified user account |

## Implementations

### ADO.NET Identity Provider - \(SanteDB.Persistence.Data.ADO\)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Persistence.Data.ADO.Services.AdoIdentityProvider, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyIdentityProviderService : SanteDB.Core.Security.Services.IIdentityProviderService { 
    public String ServiceName => "My own IIdentityProviderService service";
    /// <summary>
    /// Fired prior to an authentication event
    /// </summary>
    public event EventHandler<AuthenticatingEventArgs> Authenticating;
    /// <summary>
    /// Fired after an authentication decision being made
    /// </summary>
    public event EventHandler<AuthenticatedEventArgs> Authenticated;
    /// <summary>
    /// Retrieves an identity from the object
    /// </summary>
    public IIdentity GetIdentity(String userName){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Retrieves an identity from the object
    /// </summary>
    public IIdentity GetIdentity(Guid sid){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Create a basic identity in the provider
    /// </summary>
    public IIdentity CreateIdentity(String userName,String password,IPrincipal principal){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Authenticate the user creating an identity
    /// </summary>
    public IPrincipal Authenticate(String userName,String password){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Authenticate the user creating an identity
    /// </summary>
    public IPrincipal Authenticate(String userName,String password,String tfaSecret){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Perform a re-authentication of the principal
    /// </summary>
    public IPrincipal ReAuthenticate(IPrincipal principal){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Change user password
    /// </summary>
    public void ChangePassword(String userName,String newPassword,IPrincipal principal){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Set the user's two factor authentication secret
    /// </summary>
    public String GenerateTfaSecret(String userName){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Delete an identity
    /// </summary>
    public void DeleteIdentity(String userName,IPrincipal principal){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Set lockout
    /// </summary>
    public void SetLockout(String userName,Boolean lockout,IPrincipal principal){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Adds a claim to the specified user account
    /// </summary>
    public void AddClaim(String userName,IClaim claim,IPrincipal principal,Nullable<TimeSpan> expiriy){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Removes a claim from the specified user account
    /// </summary>
    public void RemoveClaim(String userName,String claimType,IPrincipal principal){
        throw new System.NotImplementedException();
    }
}
```


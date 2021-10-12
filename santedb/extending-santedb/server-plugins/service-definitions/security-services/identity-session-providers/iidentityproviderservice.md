---
description: IIdentityProviderService (SanteDB.Core.Api)
---

# User Identity Provider

## Summary

Identity provider service

## Events

| Event          | Type                                   | Description                                       |
| -------------- | -------------------------------------- | ------------------------------------------------- |
| Authenticating | EventHandler\<AuthenticatingEventArgs> | Fired prior to an authentication event            |
| Authenticated  | EventHandler\<AuthenticatedEventArgs>  | Fired after an authentication decision being made |

## Operations

| Operation         | Response/Return | Input/Parameter                                                                                                                                                                                           | Description                                     |
| ----------------- | --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| GetIdentity       | IIdentity       | _String_ **userName**                                                                                                                                                                                     | Retrieves an identity from the object           |
| GetIdentity       | IIdentity       | _Guid_ **sid**                                                                                                                                                                                            | Retrieves an identity from the object           |
| CreateIdentity    | IIdentity       | <p><em>String</em> <strong>userName</strong><br><em>String</em> <strong>password</strong><br><em>IPrincipal</em> <strong>principal</strong></p>                                                           | Create a basic identity in the provider         |
| Authenticate      | IPrincipal      | <p><em>String</em> <strong>userName</strong><br><em>String</em> <strong>password</strong></p>                                                                                                             | Authenticate the user creating an identity      |
| Authenticate      | IPrincipal      | <p><em>String</em> <strong>userName</strong><br><em>String</em> <strong>password</strong><br><em>String</em> <strong>tfaSecret</strong></p>                                                               | Authenticate the user creating an identity      |
| ReAuthenticate    | IPrincipal      | _IPrincipal_ **principal**                                                                                                                                                                                | Perform a re-authentication of the principal    |
| ChangePassword    | void            | <p><em>String</em> <strong>userName</strong><br><em>String</em> <strong>newPassword</strong><br><em>IPrincipal</em> <strong>principal</strong></p>                                                        | Change user password                            |
| GenerateTfaSecret | String          | _String_ **userName**                                                                                                                                                                                     | Set the user's two factor authentication secret |
| DeleteIdentity    | void            | <p><em>String</em> <strong>userName</strong><br><em>IPrincipal</em> <strong>principal</strong></p>                                                                                                        | Delete an identity                              |
| SetLockout        | void            | <p><em>String</em> <strong>userName</strong><br><em>Boolean</em> <strong>lockout</strong><br><em>IPrincipal</em> <strong>principal</strong></p>                                                           | Set lockout                                     |
| AddClaim          | void            | <p><em>String</em> <strong>userName</strong><br><em>IClaim</em> <strong>claim</strong><br><em>IPrincipal</em> <strong>principal</strong><br><em>Nullable&#x3C;TimeSpan></em> <strong>expiriy</strong></p> | Adds a claim to the specified user account      |
| RemoveClaim       | void            | <p><em>String</em> <strong>userName</strong><br><em>String</em> <strong>claimType</strong><br><em>IPrincipal</em> <strong>principal</strong></p>                                                          | Removes a claim from the specified user account |

## Implementations

### ADO.NET Identity Provider - (SanteDB.Persistence.Data.ADO)

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

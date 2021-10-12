---
description: ISecurityChallengeIdentityService (SanteDB.Core.Api)
---

# Security Challenge Identity Provider Service

## Summary

Represents a security challenge service which can provide identity

## Events

| Event          | Type                                   | Description                                       |
| -------------- | -------------------------------------- | ------------------------------------------------- |
| Authenticating | EventHandler\<AuthenticatingEventArgs> | Fired prior to an authentication event            |
| Authenticated  | EventHandler\<AuthenticatedEventArgs>  | Fired after an authentication decision being made |

## Operations

| Operation    | Response/Return | Input/Parameter                                                                                                                                                                            | Description                                                        |
| ------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------ |
| Authenticate | IPrincipal      | <p><em>String</em> <strong>userName</strong><br><em>Guid</em> <strong>challengeKey</strong><br><em>String</em> <strong>response</strong><br><em>String</em> <strong>tfaSecret</strong></p> | Authenticates the specified user with a challenge key and response |

## Implementations

### AdoSecurityChallengeProvider - (SanteDB.Persistence.Data.ADO)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Persistence.Data.ADO.Services.AdoSecurityChallengeProvider, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Security;
/// Other usings here
public class MySecurityChallengeIdentityService : SanteDB.Core.Security.ISecurityChallengeIdentityService { 
    public String ServiceName => "My own ISecurityChallengeIdentityService service";
    /// <summary>
    /// Fired prior to an authentication event
    /// </summary>
    public event EventHandler<AuthenticatingEventArgs> Authenticating;
    /// <summary>
    /// Fired after an authentication decision being made
    /// </summary>
    public event EventHandler<AuthenticatedEventArgs> Authenticated;
    /// <summary>
    /// Authenticates the specified user with a challenge key and response
    /// </summary>
    public IPrincipal Authenticate(String userName,Guid challengeKey,String response,String tfaSecret){
        throw new System.NotImplementedException();
    }
}
```

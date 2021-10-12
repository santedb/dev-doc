---
description: ISecurityChallengeService (SanteDB.Core.Api)
---

# Security Challenge Service

## Summary

Represents an interface that allows for the retrieval of pre-configured security challenges

## Operations

| Operation | Response/Return                 | Input/Parameter                                                                                                                                                                                | Description                                                           |
| --------- | ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| Get       | IEnumerable\<SecurityChallenge> | <p><em>String</em> <strong>userName</strong><br><em>IPrincipal</em> <strong>principal</strong></p>                                                                                             | Gets the challenges current registered for the user (not the answers) |
| Set       | void                            | <p><em>String</em> <strong>userName</strong><br><em>Guid</em> <strong>challengeKey</strong><br><em>String</em> <strong>response</strong><br><em>IPrincipal</em> <strong>principal</strong></p> | Add a challenge to the current registered user                        |
| Remove    | void                            | <p><em>String</em> <strong>userName</strong><br><em>Guid</em> <strong>challengeKey</strong><br><em>IPrincipal</em> <strong>principal</strong></p>                                              | Removes or clears the specified challenge                             |

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
public class MySecurityChallengeService : SanteDB.Core.Security.ISecurityChallengeService { 
    public String ServiceName => "My own ISecurityChallengeService service";
    /// <summary>
    /// Gets the challenges current registered for the user (not the answers)
    /// </summary>
    public IEnumerable<SecurityChallenge> Get(String userName,IPrincipal principal){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Add a challenge to the current registered user
    /// </summary>
    public void Set(String userName,Guid challengeKey,String response,IPrincipal principal){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Removes or clears the specified challenge
    /// </summary>
    public void Remove(String userName,Guid challengeKey,IPrincipal principal){
        throw new System.NotImplementedException();
    }
}
```

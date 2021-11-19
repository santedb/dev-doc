---
description: ISecurityRepositoryService (SanteDB.Core.Api)
---

# Security Repository

## Summary

Security repository service is responsible for the maintenance of security entities

## Operations

| Operation         | Response/Return                  | Input/Parameter                                                                                                                                                                                                                                                                                                                                    | Description                                                    |
| ----------------- | -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| ChangePassword    | SecurityUser                     | <p><em>Guid</em> <strong>userId</strong><br><em>String</em> <strong>password</strong></p>                                                                                                                                                                                                                                                          | Changes a user's password.                                     |
| GetProviderEntity | Provider                         | _IIdentity_ **identity**                                                                                                                                                                                                                                                                                                                           | Gets the specified provider entity from the specified identity |
| CreateUser        | SecurityUser                     | <p><em>SecurityUser</em> <strong>userInfo</strong><br><em>String</em> <strong>password</strong></p>                                                                                                                                                                                                                                                | Creates a user with a specified password.                      |
| GetUser           | SecurityUser                     | _String_ **userName**                                                                                                                                                                                                                                                                                                                              | Get a user by user name                                        |
| GetPolicy         | SecurityPolicy                   | _String_ **policyOid**                                                                                                                                                                                                                                                                                                                             | Get the specified security policy by OID                       |
| GetRole           | SecurityRole                     | _String_ **roleName**                                                                                                                                                                                                                                                                                                                              | Gets a specific role.                                          |
| LockDevice        | void                             | _Guid_ **key**                                                                                                                                                                                                                                                                                                                                     | Locks a device principal                                       |
| LockApplication   | void                             | _Guid_ **key**                                                                                                                                                                                                                                                                                                                                     | Locks an application                                           |
| UnlockDevice      | void                             | _Guid_ **key**                                                                                                                                                                                                                                                                                                                                     | Removes a lock from a device                                   |
| UnlockApplication | void                             | _Guid_ **key**                                                                                                                                                                                                                                                                                                                                     | Removes a lock from an application                             |
| GetUser           | SecurityUser                     | _IIdentity_ **identity**                                                                                                                                                                                                                                                                                                                           | Get a user by user name                                        |
| GetUserEntity     | UserEntity                       | _IIdentity_ **identity**                                                                                                                                                                                                                                                                                                                           | Get the user entity                                            |
| LockUser          | void                             | _Guid_ **userId**                                                                                                                                                                                                                                                                                                                                  | Locks a specific user.                                         |
| UnlockUser        | void                             | _Guid_ **userId**                                                                                                                                                                                                                                                                                                                                  | Unlocks a specific user.                                       |
| GetProvenance     | SecurityProvenance               | _Guid_ **provenanceId**                                                                                                                                                                                                                                                                                                                            | Get the provenance object                                      |
| FindProvenance    | IEnumerable\<SecurityProvenance> | <p><em>Expression&#x3C;Func&#x3C;SecurityProvenance,Boolean>></em> <strong>query</strong><br><em>Int32</em> <strong>offset</strong><br><em>Nullable&#x3C;Int32></em> <strong>count</strong><br><em>Int32&#x26;</em> <strong>totalResults</strong><br><em>Guid</em> <strong>queryId</strong><br><em>ModelSort`1[]</em> <strong>orderBy</strong></p> | Find provenance objects matching the specified object          |

## Implementations

### LocalSecurityRepositoryService - (SanteDB.Core)

Represents a security repository service that uses the direct local services

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Services.Impl.LocalSecurityRepositoryService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MySecurityRepositoryService : SanteDB.Core.Services.ISecurityRepositoryService { 
    public String ServiceName => "My own ISecurityRepositoryService service";
    /// <summary>
    /// Changes a user's password.
    /// </summary>
    public SecurityUser ChangePassword(Guid userId,String password){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Gets the specified provider entity from the specified identity
    /// </summary>
    public Provider GetProviderEntity(IIdentity identity){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Creates a user with a specified password.
    /// </summary>
    public SecurityUser CreateUser(SecurityUser userInfo,String password){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Get a user by user name
    /// </summary>
    public SecurityUser GetUser(String userName){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Get the specified security policy by OID
    /// </summary>
    public SecurityPolicy GetPolicy(String policyOid){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Gets a specific role.
    /// </summary>
    public SecurityRole GetRole(String roleName){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Locks a device principal
    /// </summary>
    public void LockDevice(Guid key){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Locks an application
    /// </summary>
    public void LockApplication(Guid key){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Removes a lock from a device
    /// </summary>
    public void UnlockDevice(Guid key){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Removes a lock from an application
    /// </summary>
    public void UnlockApplication(Guid key){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Get a user by user name
    /// </summary>
    public SecurityUser GetUser(IIdentity identity){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Get the user entity
    /// </summary>
    public UserEntity GetUserEntity(IIdentity identity){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Locks a specific user.
    /// </summary>
    public void LockUser(Guid userId){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Unlocks a specific user.
    /// </summary>
    public void UnlockUser(Guid userId){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Get the provenance object
    /// </summary>
    public SecurityProvenance GetProvenance(Guid provenanceId){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Find provenance objects matching the specified object
    /// </summary>
    public IEnumerable<SecurityProvenance> FindProvenance(Expression<Func<SecurityProvenance,Boolean>> query,Int32 offset,Nullable<Int32> count,Int32& totalResults,Guid queryId,ModelSort`1[] orderBy){
        throw new System.NotImplementedException();
    }
}
```

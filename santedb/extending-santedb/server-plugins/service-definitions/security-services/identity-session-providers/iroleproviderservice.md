---
description: IRoleProviderService (SanteDB.Core.Api)
---

# Role Provider Service

## Summary

Represents a service which is capableof retrieving roles

## Operations

| Operation            | Response/Return | Input/Parameter                                                                                                                               | Description                        |
| -------------------- | --------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| CreateRole           | void            | <p><em>String</em> <strong>roleName</strong><br><em>IPrincipal</em> <strong>principal</strong></p>                                            | Creates a role                     |
| AddUsersToRoles      | void            | <p><em>String[]</em> <strong>users</strong><br><em>String[]</em> <strong>roles</strong><br><em>IPrincipal</em> <strong>principal</strong></p> | Add users to roles                 |
| RemoveUsersFromRoles | void            | <p><em>String[]</em> <strong>users</strong><br><em>String[]</em> <strong>roles</strong><br><em>IPrincipal</em> <strong>principal</strong></p> | Remove users from specified roles  |
| FindUsersInRole      | String\[]       | _String_ **role**                                                                                                                             | Find all users in a specified role |
| GetAllRoles          | String\[]       |                                                                                                                                               | Get all roles                      |
| GetAllRoles          | String\[]       | _String_ **userName**                                                                                                                         | Get all roles                      |
| IsUserInRole         | Boolean         | <p><em>String</em> <strong>userName</strong><br><em>String</em> <strong>roleName</strong></p>                                                 | User user in the specified role    |
| IsUserInRole         | Boolean         | <p><em>IPrincipal</em> <strong>principal</strong><br><em>String</em> <strong>roleName</strong></p>                                            | User user in the specified role    |

## Implementations

### ADO.NET Role Provider Service - (SanteDB.Persistence.Data.ADO)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Persistence.Data.ADO.Services.AdoRoleProvider, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyRoleProviderService : SanteDB.Core.Security.Services.IRoleProviderService { 
    public String ServiceName => "My own IRoleProviderService service";
    /// <summary>
    /// Creates a role
    /// </summary>
    public void CreateRole(String roleName,IPrincipal principal){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Add users to roles
    /// </summary>
    public void AddUsersToRoles(String[] users,String[] roles,IPrincipal principal){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Remove users from specified roles
    /// </summary>
    public void RemoveUsersFromRoles(String[] users,String[] roles,IPrincipal principal){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Find all users in a specified role
    /// </summary>
    public String[] FindUsersInRole(String role){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Get all roles
    /// </summary>
    public String[] GetAllRoles(){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Get all roles
    /// </summary>
    public String[] GetAllRoles(String userName){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// User user in the specified role
    /// </summary>
    public Boolean IsUserInRole(String userName,String roleName){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// User user in the specified role
    /// </summary>
    public Boolean IsUserInRole(IPrincipal principal,String roleName){
        throw new System.NotImplementedException();
    }
}
```

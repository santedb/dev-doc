---
description: IAssigningAuthorityRepositoryService (SanteDB.Core.Api)
---

# Assigning Authority Repository

## Summary

Represents a repository service for managing assigning authorities.

## Operations

| Operation | Response/Return    | Input/Parameter     | Description   |
| --------- | ------------------ | ------------------- | ------------- |
| Get       | AssigningAuthority | _String_ **domain** | Get by domain |
| Get       | AssigningAuthority | _Uri_ **uri**       | Get by domain |

## Implementations

### LocalAssigningAuthorityRepository - (SanteDB.Core)

Represents a repository service for managing assigning authorities.

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Services.Impl.LocalAssigningAuthorityRepository, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyAssigningAuthorityRepositoryService : SanteDB.Core.Services.IAssigningAuthorityRepositoryService { 
    public String ServiceName => "My own IAssigningAuthorityRepositoryService service";
    /// <summary>
    /// Get by domain
    /// </summary>
    public AssigningAuthority Get(String domain){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Get by domain
    /// </summary>
    public AssigningAuthority Get(Uri uri){
        throw new System.NotImplementedException();
    }
}
```

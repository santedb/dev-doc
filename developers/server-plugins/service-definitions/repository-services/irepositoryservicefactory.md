---
description: IRepositoryServiceFactory (SanteDB.Core.Api)
---

# Repository Factory Service

## Summary

Represents a factory service which can be used to generate default factories

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| CreateRepository | IRepositoryService&lt;T&gt; |  | TODO |

## Implementations

### Local Data Repository Factory - \(SanteDB.Core\)

Represents a generic resource repository factory

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Services.Impl.LocalRepositoryFactoryService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyRepositoryServiceFactory : SanteDB.Core.Services.IRepositoryServiceFactory { 
    public String ServiceName => "My own IRepositoryServiceFactory service";
    public IRepositoryService<T> CreateRepository<T>(){
        throw new System.NotImplementedException();
    }
}
```


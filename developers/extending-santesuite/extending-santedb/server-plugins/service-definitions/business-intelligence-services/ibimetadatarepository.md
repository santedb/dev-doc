---
description: IBiMetadataRepository (SanteDB.BI)
---

# BI Metadata Repository

## Summary

Represents a metadata repository for the BIS services

## Operations

| Operation | Response/Return              | Input/Parameter                                                                                                                                                                              | Description                                             |
| --------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| Query     | IEnumerable\<TBisDefinition> | <p><em>Expression&#x3C;Func&#x3C;TBisDefinition,Boolean>></em> <strong>filter</strong><br><em>Int32</em> <strong>offset</strong><br><em>Nullable&#x3C;Int32></em> <strong>count</strong></p> | Query metadata repository for                           |
| Get       | TBisDefinition               | _String_ **id**                                                                                                                                                                              | Get the specified BI definition by identifier           |
| Remove    | void                         | _String_ **id**                                                                                                                                                                              | Removes the specified BI definition from the repository |
| Insert    | TBisDefinition               | _TBisDefinition_ **metadata**                                                                                                                                                                | Inserts the specified BI definition into the repository |

## Implementations

### AppletBiRepository - (SanteDB.BI)

Represents a default implementation of a BIS metadata repository which loads definitions from loaded applets

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.BI.Services.Impl.AppletBiRepository, SanteDB.BI, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### File Based BI Repository - (SanteDB.Tools.Debug)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Tools.Debug.BI.FileMetadataRepository, SanteDB.Tools.Debug, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.BI.Services;
/// Other usings here
public class MyBiMetadataRepository : SanteDB.BI.Services.IBiMetadataRepository { 
    public String ServiceName => "My own IBiMetadataRepository service";
    /// <summary>
    /// Query metadata repository for
    /// </summary>
    public IEnumerable<TBisDefinition> Query<TBisDefinition>(Expression<Func<TBisDefinition,Boolean>> filter,Int32 offset,Nullable<Int32> count){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Get the specified BI definition by identifier
    /// </summary>
    public TBisDefinition Get<TBisDefinition>(String id){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Removes the specified BI definition from the repository
    /// </summary>
    public void Remove<TBisDefinition>(String id){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Inserts the specified BI definition into the repository
    /// </summary>
    public TBisDefinition Insert<TBisDefinition>(TBisDefinition metadata){
        throw new System.NotImplementedException();
    }
}
```

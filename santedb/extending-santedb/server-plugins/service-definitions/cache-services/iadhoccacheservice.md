---
description: IAdhocCacheService (SanteDB.Core.Api)
---

# Adhoc Cache Service

## Summary

A caching service which permits the storage of any data regardless of type

## Operations

| Operation | Response/Return | Input/Parameter                                                                                                                               | Description                              |
| --------- | --------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| Add       | void            | <p><em>String</em> <strong>key</strong><br><em>T</em> <strong>value</strong><br><em>Nullable&#x3C;TimeSpan></em> <strong>timeout</strong></p> | Add the specified object to the cache    |
| Get       | T               | _String_ **key**                                                                                                                              | Gets the specified object from the cache |

## Implementations

### RedisAdhocCache - (SanteDB.Caching.Redis)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Caching.Redis.RedisAdhocCache, SanteDB.Caching.Redis, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyAdhocCacheService : SanteDB.Core.Services.IAdhocCacheService { 
    public String ServiceName => "My own IAdhocCacheService service";
    /// <summary>
    /// Add the specified object to the cache
    /// </summary>
    public void Add<T>(String key,T value,Nullable<TimeSpan> timeout){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Gets the specified object from the cache
    /// </summary>
    public T Get<T>(String key){
        throw new System.NotImplementedException();
    }
}
```

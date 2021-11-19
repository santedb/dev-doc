---
description: IDataCachingService (SanteDB.Core.Api)
---

# Data Caching Service

## Summary

Represents a data caching service which allows services to retrieve cached objects

## Events

| Event | Type | Description |
| :--- | :--- | :--- |
| Added | EventHandler&lt;DataCacheEventArgs&gt; | Item was added to cache |
| Updated | EventHandler&lt;DataCacheEventArgs&gt; | Item was updated from cache |
| Removed | EventHandler&lt;DataCacheEventArgs&gt; | Item was removed from cache |

## Properties

| Property | Type | Access | Description |
| :--- | :--- | :--- | :--- |
| Size | Int64 | R | Gets the current size of the cache |

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| GetCacheItem | TData | _Guid_ **key** | Get the specified cache item |
| GetCacheItem | Object | _Guid_ **key** | Gets the specified cache item |
| Add | void | _IdentifiedData_ **data** | Adds the specified item to the cache |
| Remove | void | _Guid_ **key** | Removes an object from the cache |
| Clear | void |  | TODO |

## Implementations

### Memory Cache Service - \(SanteDB.Caching.Memory\)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Caching.Memory.MemoryCacheService, SanteDB.Caching.Memory, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### REDIS Data Caching Service - \(SanteDB.Caching.Redis\)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Caching.Redis.RedisCacheService, SanteDB.Caching.Redis, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyDataCachingService : SanteDB.Core.Services.IDataCachingService { 
    public String ServiceName => "My own IDataCachingService service";
    /// <summary>
    /// Item was added to cache
    /// </summary>
    public event EventHandler<DataCacheEventArgs> Added;
    /// <summary>
    /// Item was updated from cache
    /// </summary>
    public event EventHandler<DataCacheEventArgs> Updated;
    /// <summary>
    /// Item was removed from cache
    /// </summary>
    public event EventHandler<DataCacheEventArgs> Removed;
    /// <summary>
    /// Gets the current size of the cache
    /// </summary>
    public Int64 Size {
        get;
    }
    /// <summary>
    /// Get the specified cache item
    /// </summary>
    public TData GetCacheItem<TData>(Guid key){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Gets the specified cache item
    /// </summary>
    public Object GetCacheItem(Guid key){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Adds the specified item to the cache
    /// </summary>
    public void Add(IdentifiedData data){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Removes an object from the cache
    /// </summary>
    public void Remove(Guid key){
        throw new System.NotImplementedException();
    }
    public void Clear(){
        throw new System.NotImplementedException();
    }
}
```


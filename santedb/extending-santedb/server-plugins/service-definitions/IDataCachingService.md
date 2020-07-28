---
description: IDataCachingService (SanteDB.Core.Api)
---

## Summary
Represents a data caching service which allows services to retrieve
            cached objects

## Events

|Event|Type|Description|
|-|-|-|
|Added|System.EventHandler<SanteDB.Core.Services.DataCacheEventArgs>|Item was added to cache|
|Updated|System.EventHandler<SanteDB.Core.Services.DataCacheEventArgs>|Item was updated from cache|
|Removed|System.EventHandler<SanteDB.Core.Services.DataCacheEventArgs>|Item was removed from cache|

## Properties


## Methods


## Implementations


### Memory Cache Service - (SanteDB.Caching.Memory)
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

### REDIS Data Caching Service - (SanteDB.Caching.Redis)
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
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyDataCachingService : SanteDB.Core.Services.IDataCachingService { 
	public String ServiceName => "My own IDataCachingService service";
	/// <summary>
	/// Item was added to cache
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Services.DataCacheEventArgs> Added;
	/// <summary>
	/// Item was updated from cache
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Services.DataCacheEventArgs> Updated;
	/// <summary>
	/// Item was removed from cache
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Services.DataCacheEventArgs> Removed;
	/// <summary>
	/// Gets the current size of the cache
	/// </summary>
	public System.Int64 Size {
		get;
	}
	/// <summary>
	/// Get the specified cache item
	/// </summary>
	public TData GetCacheItem<TData>(System.Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified cache item
	/// </summary>
	public System.Object GetCacheItem(System.Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Adds the specified item to the cache
	/// </summary>
	public void Add(SanteDB.Core.Model.IdentifiedData data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes an object from the cache
	/// </summary>
	public void Remove(System.Guid key){
		throw new System.NotImplementedException();
	}
	public void Clear(){
		throw new System.NotImplementedException();
	}
}
```

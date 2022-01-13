`IDataCachingService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Defines a service which can be used by callers to store full [IdentifiedData](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_IdentifiedData.htm) RIM objects
            in a transient cache.

## Description
The data caching service is primarily used to store fully loaded objects from the database. This loading into the cache
            reduces the load on the persistence layer of the SanteDB host context. The data persistence layers themselves will use implementations
            of this class to prevent re-loading of data to/from the disk system. The process on a read is generally: 

1. Check the cache service to determine if the data has already been loaded
1. If not found in cache load the data from disk / database
1. Add the object to the cache


Of course, keeping the cache service in a consistent state is tantamount to the reliable functioning of SanteDB, this means that any update, delete or create on
            an object that already exists in cache results in its eviction from the cache via the [Guid)](#Guid)) method.

# Events

|Event|Type|Description|
|-|-|-|
|Added|EventHandler&lt;DataCacheEventArgs>|Fired after an object has successfully been committed to the cache|
|Updated|EventHandler&lt;DataCacheEventArgs>|Fired after an object has successfully been updated within the cache|
|Removed|EventHandler&lt;DataCacheEventArgs>|Fired after an object has successfully been evicted from cache|

# Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Size|Int64|R|Gets the current size of the cache in objects|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetCacheItem|TData|*Guid* **key**|Gets the cache item specified by  returning it as a casted instance of . Returning the default of  if the            object doesn't exist or if the object is the wrong type.|
|GetCacheItem|IdentifiedData|*Guid* **key**|Gets the cache item specified by  regardless of the type of data|
|Add|void|*IdentifiedData* **data**|Adds  to the cache|
|Remove|void|*Guid* **key**|Removes/evicts an object with identifier  from the cache|
|Remove|void|*IdentifiedData* **data**|Removes/evicts an object with identifier  from the cache|
|Clear|void||TODO|

# Implementations


## Memory Cache Service - (SanteDB.Caching.Memory)
Implementation of the [IDataCachingService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataCachingService.htm) which uses the in-process memory to cache objects
### Description
The memory cache service uses the [MemoryCache](https://docs.microsoft.com/en-us/dotnet/api/system.runtime.caching.memorycache) class as a backing cache
            for the SanteDB host instance. This caching provider provides benefits over a common, shared cache like REDIS in that:

* It does not require the setup of a third-party service to operate
* The cache objects are directly accessed and not serialized
* The cache objects are protected within the host process memory
* The access is very fast - there is no interconnection with another process


This cache service should only be used in cases when there is a single SanteDB server and there is no need
            for sharing cache objects between application services.

This class uses the TTL setting from the [MemoryCacheConfigurationSection](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Memory_Configuration_MemoryCacheConfigurationSection.htm) to determine the length of time
            that cache entries are valid

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Caching.Memory.MemoryCacheService, SanteDB.Caching.Memory, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## REDIS Data Caching Service - (SanteDB.Caching.Redis)
An implementation of the [IDataCachingService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataCachingService.htm) which uses REDIS
### Description
This implementation of the caching service uses the XMLSerializer in .NET to serialize any object passed in
            via the [IdentifiedData)](#IdentifiedData)) method. The data is then compressed (if configured) and sent to the
            configured REDIS server.

The use of the .NET XML serializer over the Newtonsoft JSON serializer for caching was chosen since the
            serializer operates on streams (saves string conversions) and pre-compiles the serialization classes on .NET Framework implementations
            (Mono implementations use relfection)

The caching data is stored in database 1 of the REDIS server.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Caching.Redis.RedisCacheService, SanteDB.Caching.Redis, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyDataCachingService : SanteDB.Core.Services.IDataCachingService { 
	public String ServiceName => "My own IDataCachingService service";
	/// <summary>
	/// Fired after an object has successfully been committed to the cache
	/// </summary>
	public event EventHandler<DataCacheEventArgs> Added;
	/// <summary>
	/// Fired after an object has successfully been updated within the cache
	/// </summary>
	public event EventHandler<DataCacheEventArgs> Updated;
	/// <summary>
	/// Fired after an object has successfully been evicted from cache
	/// </summary>
	public event EventHandler<DataCacheEventArgs> Removed;
	/// <summary>
	/// Gets the current size of the cache in objects
	/// </summary>
	public Int64 Size {
		get;
	}
	/// <summary>
	/// Gets the cache item specified by  returning it as a casted instance of . Returning the default of  if the            object doesn't exist or if the object is the wrong type.
	/// </summary>
	public TData GetCacheItem<TData>(Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the cache item specified by  regardless of the type of data
	/// </summary>
	public IdentifiedData GetCacheItem(Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Adds  to the cache
	/// </summary>
	public void Add(IdentifiedData data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes/evicts an object with identifier  from the cache
	/// </summary>
	public void Remove(Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes/evicts an object with identifier  from the cache
	/// </summary>
	public void Remove(IdentifiedData data){
		throw new System.NotImplementedException();
	}
	public void Clear(){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDataCachingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataCachingService.htm)
* [MemoryCacheService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Memory_MemoryCacheService.htm)
* [RedisCacheService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Redis_RedisCacheService.htm)

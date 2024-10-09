`IAdhocCacheService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Defines a service which can store commonly used objects in a transient cache

## Description
The ad-hoc cache service differs from the data cache in that the ad-hoc cache can be used to store any data with any
             key and value within the caching technology implementation. The cache is commonly used to store repeat or commonly
             fetched data (for example policy decision outcomes, keys, reference term lookups, etc.).

The cache can be used to save fetching and querying data to/from the persistence layer.

Note to Implementers: Your implementation of this interface should not be a persistent cache (if possible to enforce). The
             callers of this interface typically assume a short lifecycle of data within the cache, and transient, rapid access should be prioritized over
             durability.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Add|void|*String* **key**<br/>*T* **value**<br/>*Nullable&lt;TimeSpan>* **timeout**|Add the specified object to the cache|
|Get|T|*String* **key**|Gets the specified object from the cache|
|TryGet|Boolean|*String* **key**<br/>*T&* **value**|Try to fetch  from the cache|
|Remove|Boolean|*String* **key**|Removes the specified object from the adhoc|
|RemoveAll|void|*String* **patternKey**|Remove all keys matching|
|Exists|Boolean|*String* **key**|Returns true if  exists in the cache|

# Implementations


## Memory Ad-Hoc Cache Service - (SanteDB.Caching.Memory)
An implementation of [IAdhocCacheService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IAdhocCacheService.htm) which uses the in-process memory cache
### Description
This implementation of the adhoc caching service uses in-process memory to store unstructured data
            which is commonly used in the application.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Caching.Memory.MemoryAdhocCacheService, SanteDB.Caching.Memory, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## RedisAdhocCache - (SanteDB.Caching.Redis)
An implementation of the [IAdhocCacheService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IAdhocCacheService.htm) which uses REDIS as the cache provider
### Description
This implementation of the REDIS ad-hoc cache provider serializes any data passed via [TimeSpan})](#TimeSpan})) to a JSON representation, then
            compresses (optional) the data and stores it in REDIS as a simple string

The data is stored in database 3 of the REDIS server

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Caching.Redis.RedisAdhocCache, SanteDB.Caching.Redis, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
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
	/// <summary>
	/// Try to fetch  from the cache
	/// </summary>
	public Boolean TryGet<T>(String key,T& value){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes the specified object from the adhoc
	/// </summary>
	public Boolean Remove(String key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Remove all keys matching
	/// </summary>
	public void RemoveAll(String patternKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Returns true if  exists in the cache
	/// </summary>
	public Boolean Exists(String key){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IAdhocCacheService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IAdhocCacheService.htm)
* [MemoryAdhocCacheService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Memory_MemoryAdhocCacheService.htm)
* [RedisAdhocCache C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Redis_RedisAdhocCache.htm)

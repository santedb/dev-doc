---
description: IAdhocCacheService (SanteDB.Core.Api)
---

## Summary
A caching service which permits the storage of any data regardless of type

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Add|void|key <small style='border:solid 1px #aaa'>String</small><br/>value <small style='border:solid 1px #aaa'>T</small><br/>timeout <small style='border:solid 1px #aaa'>Nullable<TimeSpan></small>|Add the specified object to the cache|
|Get|T|key <small style='border:solid 1px #aaa'>String</small>|Gets the specified object from the cache|

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
## Example
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

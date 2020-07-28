---
description: IQueryPersistenceService (SanteDB.Core.Api)
---

## Summary
Query persistence service

## Implementations


### Memory-Based Query Persistence Service - (SanteDB.Caching.Memory)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Caching.Memory.MemoryQueryPersistenceService, SanteDB.Caching.Memory, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

### REDIS Query Persistence Service - (SanteDB.Caching.Redis)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Caching.Redis.RedisQueryPersistenceService, SanteDB.Caching.Redis, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyQueryPersistenceService : SanteDB.Core.Services.IQueryPersistenceService { 
	public String ServiceName => "My own IQueryPersistenceService service";
	/// <summary>
	/// Find the query ID by the query tag
	/// </summary>
	public System.Guid FindQueryId(System.Object queryTag){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Register a query set
	/// </summary>
	public System.Boolean RegisterQuerySet(System.Guid queryId,System.Collections.Generic.IEnumerable<System.Guid> results,System.Object tag,System.Int32 totalResults){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Returns true if the query identifier is already registered
	/// </summary>
	public System.Boolean IsRegistered(System.Guid queryId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get query results from the query set result store
	/// </summary>
	public System.Collections.Generic.IEnumerable<System.Guid> GetQueryResults(System.Guid queryId,System.Int32 offset,System.Int32 count){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the query tag value from the result store
	/// </summary>
	public System.Object GetQueryTag(System.Guid queryId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Count the number of remaining query results
	/// </summary>
	public System.Int64 QueryResultTotalQuantity(System.Guid queryId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Add results to the query
	/// </summary>
	public void AddResults(System.Guid queryId,System.Collections.Generic.IEnumerable<System.Guid> results){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Set or update the query tag of an existing query id
	/// </summary>
	public void SetQueryTag(System.Guid queryId,System.Object value){
		throw new System.NotImplementedException();
	}
}
```

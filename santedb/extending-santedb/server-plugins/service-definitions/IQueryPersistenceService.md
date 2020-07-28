---
description: IQueryPersistenceService (SanteDB.Core.Api)
---

## Summary
Query persistence service

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|FindQueryId|Guid|*Object* **queryTag**|Find the query ID by the query tag|
|RegisterQuerySet|Boolean|*Guid* **queryId**<br/>*IEnumerable&lt;Guid>* **results**<br/>*Object* **tag**<br/>*Int32* **totalResults**|Register a query set|
|IsRegistered|Boolean|*Guid* **queryId**|Returns true if the query identifier is already registered|
|GetQueryResults|IEnumerable&lt;Guid>|*Guid* **queryId**<br/>*Int32* **offset**<br/>*Int32* **count**|Get query results from the query set result store|
|GetQueryTag|Object|*Guid* **queryId**|Get the query tag value from the result store|
|QueryResultTotalQuantity|Int64|*Guid* **queryId**|Count the number of remaining query results|
|AddResults|void|*Guid* **queryId**<br/>*IEnumerable&lt;Guid>* **results**|Add results to the query|
|SetQueryTag|void|*Guid* **queryId**<br/>*Object* **value**|Set or update the query tag of an existing query id|

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
	public Guid FindQueryId(Object queryTag){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Register a query set
	/// </summary>
	public Boolean RegisterQuerySet(Guid queryId,IEnumerable<Guid> results,Object tag,Int32 totalResults){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Returns true if the query identifier is already registered
	/// </summary>
	public Boolean IsRegistered(Guid queryId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get query results from the query set result store
	/// </summary>
	public IEnumerable<Guid> GetQueryResults(Guid queryId,Int32 offset,Int32 count){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the query tag value from the result store
	/// </summary>
	public Object GetQueryTag(Guid queryId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Count the number of remaining query results
	/// </summary>
	public Int64 QueryResultTotalQuantity(Guid queryId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Add results to the query
	/// </summary>
	public void AddResults(Guid queryId,IEnumerable<Guid> results){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Set or update the query tag of an existing query id
	/// </summary>
	public void SetQueryTag(Guid queryId,Object value){
		throw new System.NotImplementedException();
	}
}
```

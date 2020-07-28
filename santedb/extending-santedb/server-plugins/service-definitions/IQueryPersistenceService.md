---
description: IQueryPersistenceService (SanteDB.Core.Api)
---

## Summary
Query persistence service

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|FindQueryId|System.Guid|queryTag <small style='border:solid 1px #aaa'>System.Object</small>|Find the query ID by the query tag|
|RegisterQuerySet|System.Boolean|queryId <small style='border:solid 1px #aaa'>System.Guid</small><br/>results <small style='border:solid 1px #aaa'>System.Collections.Generic.IEnumerable<System.Guid></small><br/>tag <small style='border:solid 1px #aaa'>System.Object</small><br/>totalResults <small style='border:solid 1px #aaa'>System.Int32</small>|Register a query set|
|IsRegistered|System.Boolean|queryId <small style='border:solid 1px #aaa'>System.Guid</small>|Returns true if the query identifier is already registered|
|GetQueryResults|System.Collections.Generic.IEnumerable&lt;System.Guid>|queryId <small style='border:solid 1px #aaa'>System.Guid</small><br/>offset <small style='border:solid 1px #aaa'>System.Int32</small><br/>count <small style='border:solid 1px #aaa'>System.Int32</small>|Get query results from the query set result store|
|GetQueryTag|System.Object|queryId <small style='border:solid 1px #aaa'>System.Guid</small>|Get the query tag value from the result store|
|QueryResultTotalQuantity|System.Int64|queryId <small style='border:solid 1px #aaa'>System.Guid</small>|Count the number of remaining query results|
|AddResults|void|queryId <small style='border:solid 1px #aaa'>System.Guid</small><br/>results <small style='border:solid 1px #aaa'>System.Collections.Generic.IEnumerable<System.Guid></small>|Add results to the query|
|SetQueryTag|void|queryId <small style='border:solid 1px #aaa'>System.Guid</small><br/>value <small style='border:solid 1px #aaa'>System.Object</small>|Set or update the query tag of an existing query id|

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

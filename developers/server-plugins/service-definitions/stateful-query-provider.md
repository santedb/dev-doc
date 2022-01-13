`IQueryPersistenceService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Defines a service which can store the results of a query for later retrieval

## Description
When implementing query on a shared infrastructure such as the SanteDB iCDR or dCDR, it is important that consistent result sets be returned. This is
            important not only for user interfaces, but is vital to consistent synchronization across devices.

There are several reasons we keep stateful query result sets in SanteDB:

* User interfaces will have consistent pages, so results don't magically "appear" between paging results
* Synchronization processes have a consistent paging result set as they download data
* The heavy initial query is done only once and results are merely accessed afterwards


Implementers of this service should ensure that whatever technology they are using to store queries have the capability of expiration (i.e. queries are
            not stateful indefinitely), support the rapid read and update of result sets, and are cabable of being aborted/abandoned.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|FindQueryId|Guid|*Object* **queryTag**|Locate the stateful query identifier using the tag which was attached to the query|
|RegisterQuerySet|Boolean|*Guid* **queryId**<br/>*IEnumerable&lt;Guid>* **results**<br/>*Object* **tag**<br/>*Int32* **totalResults**|Registers a new query result set with the stateful query provider|
|IsRegistered|Boolean|*Guid* **queryId**|Returns true if the query identifier has been registered|
|GetQueryResults|IEnumerable&lt;Guid>|*Guid* **queryId**<br/>*Int32* **offset**<br/>*Int32* **count**|Retrieves the result keys located between  and + in the stateful query provider|
|GetQueryTag|Object|*Guid* **queryId**|Retrieves the query tag stored when the query was registered, for the specified|
|QueryResultTotalQuantity|Int64|*Guid* **queryId**|Count the number of query results which have been registered for|
|AddResults|void|*Guid* **queryId**<br/>*IEnumerable&lt;Guid>* **results**<br/>*Int32* **totalResults**|Adds more results to an already registered stateful query|
|SetQueryTag|void|*Guid* **queryId**<br/>*Object* **value**|Adds or changes the query tag on  to|

# Implementations


## Memory-Based Query Persistence Service - (SanteDB.Caching.Memory)
An implementation of the [IQueryPersistenceService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IQueryPersistenceService.htm) which uses in-process memory to store query result sets
### Description
This implementation of the query persistence service uses the [MemoryCache](https://docs.microsoft.com/en-us/dotnet/api/system.runtime.caching.memorycache) implementation to store
            stateful query results (for consistent pagination) for a period of time in transient place.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Caching.Memory.MemoryQueryPersistenceService, SanteDB.Caching.Memory, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## REDIS Query Persistence Service - (SanteDB.Caching.Redis)
An implementation of the [IQueryPersistenceService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IQueryPersistenceService.htm) which usees REDIS for its stateful result set
### Description
This persistence service uses REDIS list values to store the UUIDs representing the query executed on the SanteDB server. The data
            is stored in database 2 of the REDIS server.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Caching.Redis.RedisQueryPersistenceService, SanteDB.Caching.Redis, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyQueryPersistenceService : SanteDB.Core.Services.IQueryPersistenceService { 
	public String ServiceName => "My own IQueryPersistenceService service";
	/// <summary>
	/// Locate the stateful query identifier using the tag which was attached to the query
	/// </summary>
	public Guid FindQueryId(Object queryTag){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Registers a new query result set with the stateful query provider
	/// </summary>
	public Boolean RegisterQuerySet(Guid queryId,IEnumerable<Guid> results,Object tag,Int32 totalResults){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Returns true if the query identifier has been registered
	/// </summary>
	public Boolean IsRegistered(Guid queryId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Retrieves the result keys located between  and + in the stateful query provider
	/// </summary>
	public IEnumerable<Guid> GetQueryResults(Guid queryId,Int32 offset,Int32 count){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Retrieves the query tag stored when the query was registered, for the specified
	/// </summary>
	public Object GetQueryTag(Guid queryId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Count the number of query results which have been registered for
	/// </summary>
	public Int64 QueryResultTotalQuantity(Guid queryId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Adds more results to an already registered stateful query
	/// </summary>
	public void AddResults(Guid queryId,IEnumerable<Guid> results,Int32 totalResults){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Adds or changes the query tag on  to
	/// </summary>
	public void SetQueryTag(Guid queryId,Object value){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IQueryPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IQueryPersistenceService.htm)
* [MemoryQueryPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Memory_MemoryQueryPersistenceService.htm)
* [RedisQueryPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Redis_RedisQueryPersistenceService.htm)

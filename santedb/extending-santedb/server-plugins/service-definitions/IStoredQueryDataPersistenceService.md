---
description: IStoredQueryDataPersistenceService<TEntity> (SanteDB.Core.Api)
---

## Summary
Represents a data persistence provider that can store and continue queries

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Query|IEnumerable&lt;TEntity>|*Expression&lt;Func&lt;TEntity,Boolean>>* **query**<br/>*Guid* **queryId**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalCount**<br/>*IPrincipal* **overrideAuthContext**<br/>*ModelSort`1[]* **orderBy**|Queries or continues a query|

## Implementations

None

## Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyStoredQueryDataPersistenceService<TEntity> : SanteDB.Core.Services.IStoredQueryDataPersistenceService<TEntity> { 
	public String ServiceName => "My own IStoredQueryDataPersistenceService`1 service";
	/// <summary>
	/// Queries or continues a query
	/// </summary>
	public IEnumerable<TEntity> Query(Expression<Func<TEntity,Boolean>> query,Guid queryId,Int32 offset,Nullable<Int32> count,Int32& totalCount,IPrincipal overrideAuthContext,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
}
```

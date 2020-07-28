---
description: IPersistableQueryRepositoryService<TEntity> (SanteDB.Core.Api)
---

## Summary
Persistable query provider is an extensable interface which can perform a query with state

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Find|IEnumerable&lt;TEntity>|*Expression&lt;Func&lt;TEntity,Boolean>>* **query**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**<br/>*Guid* **queryId**<br/>*ModelSort`1[]* **orderBy**|Performs a query which|

## Implementations

None

## Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyPersistableQueryRepositoryService<TEntity> : SanteDB.Core.Services.IPersistableQueryRepositoryService<TEntity> { 
	public String ServiceName => "My own IPersistableQueryRepositoryService`1 service";
	/// <summary>
	/// Performs a query which
	/// </summary>
	public IEnumerable<TEntity> Find(Expression<Func<TEntity,Boolean>> query,Int32 offset,Nullable<Int32> count,Int32& totalResults,Guid queryId,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
}
```

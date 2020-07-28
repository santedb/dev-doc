---
description: IFastQueryRepositoryService<TEntity> (SanteDB.Core.Api)
---

## Summary
Represents a query repository service which can find lean queries

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|FindFast|IEnumerable&lt;TEntity>|*Expression&lt;Func&lt;TEntity,Boolean>>* **query**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**<br/>*Guid* **queryId**|Perform a quick search (instructs the data persistence layer not to load as many properties)|

## Implementations

None

## Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyFastQueryRepositoryService<TEntity> : SanteDB.Core.Services.IFastQueryRepositoryService<TEntity> { 
	public String ServiceName => "My own IFastQueryRepositoryService`1 service";
	/// <summary>
	/// Perform a quick search (instructs the data persistence layer not to load as many properties)
	/// </summary>
	public IEnumerable<TEntity> FindFast(Expression<Func<TEntity,Boolean>> query,Int32 offset,Nullable<Int32> count,Int32& totalResults,Guid queryId){
		throw new System.NotImplementedException();
	}
}
```

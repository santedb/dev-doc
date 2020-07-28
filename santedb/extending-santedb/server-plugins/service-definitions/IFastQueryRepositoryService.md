---
description: IFastQueryRepositoryService`1 (SanteDB.Core.Api)
---

## Summary
Represents a query repository service which can find lean queries

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyFastQueryRepositoryService<TEntity> : SanteDB.Core.Services.IFastQueryRepositoryService<TEntity> { 
	public String ServiceName => "My own IFastQueryRepositoryService`1 service";
	/// <summary>
	/// Perform a quick search (instructs the data persistence layer not to load as many properties)
	/// </summary>
	public System.Collections.Generic.IEnumerable<TEntity> FindFast(System.Linq.Expressions.Expression<System.Func<TEntity,System.Boolean>> query,System.Int32 offset,System.Nullable<System.Int32> count,System.Int32& totalResults,System.Guid queryId){
		throw new System.NotImplementedException();
	}
}
```

---
description: IPersistableQueryRepositoryService`1 (SanteDB.Core.Api)
---

## Summary
Persistable query provider is an extensable interface which can perform a query with state

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyPersistableQueryRepositoryService<TEntity> : SanteDB.Core.Services.IPersistableQueryRepositoryService<TEntity> { 
	public String ServiceName => "My own IPersistableQueryRepositoryService`1 service";
	/// <summary>
	/// Performs a query which
	/// </summary>
	public System.Collections.Generic.IEnumerable<TEntity> Find(System.Linq.Expressions.Expression<System.Func<TEntity,System.Boolean>> query,System.Int32 offset,System.Nullable<System.Int32> count,System.Int32& totalResults,System.Guid queryId, orderBy){
		throw new System.NotImplementedException();
	}
}
```

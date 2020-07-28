---
description: IStoredQueryDataPersistenceService`1 (SanteDB.Core.Api)
---

## Summary
Represents a data persistence provider that can store and continue queries

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyStoredQueryDataPersistenceService<TEntity> : SanteDB.Core.Services.IStoredQueryDataPersistenceService<TEntity> { 
	public String ServiceName => "My own IStoredQueryDataPersistenceService`1 service";
	/// <summary>
	/// Queries or continues a query
	/// </summary>
	public System.Collections.Generic.IEnumerable<TEntity> Query(System.Linq.Expressions.Expression<System.Func<TEntity,System.Boolean>> query,System.Guid queryId,System.Int32 offset,System.Nullable<System.Int32> count,System.Int32& totalCount,System.Security.Principal.IPrincipal overrideAuthContext, orderBy){
		throw new System.NotImplementedException();
	}
}
```

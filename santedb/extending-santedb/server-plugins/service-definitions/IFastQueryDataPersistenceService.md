---
description: IFastQueryDataPersistenceService`1 (SanteDB.Core.Api)
---

## Summary
Data persistence service lean mode

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyFastQueryDataPersistenceService<TEntity> : SanteDB.Core.Services.IFastQueryDataPersistenceService<TEntity> { 
	public String ServiceName => "My own IFastQueryDataPersistenceService`1 service";
	/// <summary>
	/// Queries or continues a query in lean mode
	/// </summary>
	public System.Collections.Generic.IEnumerable<TEntity> QueryFast(System.Linq.Expressions.Expression<System.Func<TEntity,System.Boolean>> query,System.Guid queryId,System.Int32 offset,System.Nullable<System.Int32> count,System.Int32& totalCount,System.Security.Principal.IPrincipal overrideAuthContext){
		throw new System.NotImplementedException();
	}
}
```

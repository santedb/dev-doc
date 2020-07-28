---
description: IFreetextSearchService (SanteDB.Core.Api)
---

## Summary
Free text search service

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyFreetextSearchService : SanteDB.Core.Services.IFreetextSearchService { 
	public String ServiceName => "My own IFreetextSearchService service";
	/// <summary>
	/// Search based on tokens
	/// </summary>
	public System.Collections.Generic.IEnumerable<TEntity> Search<TEntity>(System.String[] term,System.Int32 offset,System.Nullable<System.Int32> count,System.Int32& totalResults, orderBy){
		throw new System.NotImplementedException();
	}
}
```

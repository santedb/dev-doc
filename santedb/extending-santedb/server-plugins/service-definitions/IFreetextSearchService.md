---
description: IFreetextSearchService (SanteDB.Core.Api)
---

## Summary
Free text search service

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Search|IEnumerable&lt;TEntity>|*String[]* **term**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**<br/>*ModelSort`1[]* **orderBy**|Search based on tokens|

## Implementations

None

## Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyFreetextSearchService : SanteDB.Core.Services.IFreetextSearchService { 
	public String ServiceName => "My own IFreetextSearchService service";
	/// <summary>
	/// Search based on tokens
	/// </summary>
	public IEnumerable<TEntity> Search<TEntity>(String[] term,Int32 offset,Nullable<Int32> count,Int32& totalResults,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
}
```

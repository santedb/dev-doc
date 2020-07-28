---
description: IFreetextSearchService (SanteDB.Core.Api)
---

## Summary
Free text search service

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Search|System.Collections.Generic.IEnumerable&lt;TEntity>|term <small style='border:solid 1px #aaa'>System.String[]</small><br/>offset <small style='border:solid 1px #aaa'>System.Int32</small><br/>count <small style='border:solid 1px #aaa'>System.Nullable<System.Int32></small><br/>totalResults <small style='border:solid 1px #aaa'>System.Int32&</small><br/>orderBy <small style='border:solid 1px #aaa'></small>|Search based on tokens|

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

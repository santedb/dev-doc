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
|Search|IEnumerable&lt;TEntity>|term <small style='border:solid 1px #aaa'>String[]</small><br/>offset <small style='border:solid 1px #aaa'>Int32</small><br/>count <small style='border:solid 1px #aaa'>Nullable<Int32></small><br/>totalResults <small style='border:solid 1px #aaa'>Int32&</small><br/>orderBy <small style='border:solid 1px #aaa'>ModelSort`1[]</small>|Search based on tokens|

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
	public IEnumerable<TEntity> Search<TEntity>(String[] term,Int32 offset,Nullable<Int32> count,Int32& totalResults,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
}
```

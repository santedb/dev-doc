---
description: IFastQueryRepositoryService`1 (SanteDB.Core.Api)
---

## Summary
Represents a query repository service which can find lean queries

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|FindFast|System.Collections.Generic.IEnumerable&lt;TEntity>|query <small style='border:solid 1px #aaa'>System.Linq.Expressions.Expression<System.Func<TEntity,System.Boolean>></small><br/>offset <small style='border:solid 1px #aaa'>System.Int32</small><br/>count <small style='border:solid 1px #aaa'>System.Nullable<System.Int32></small><br/>totalResults <small style='border:solid 1px #aaa'>System.Int32&</small><br/>queryId <small style='border:solid 1px #aaa'>System.Guid</small>|Perform a quick search (instructs the data persistence layer not to load as many properties)|

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

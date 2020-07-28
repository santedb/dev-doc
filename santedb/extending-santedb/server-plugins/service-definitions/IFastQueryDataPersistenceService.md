---
description: IFastQueryDataPersistenceService<TEntity> (SanteDB.Core.Api)
---

## Summary
Data persistence service lean mode

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|QueryFast|IEnumerable&lt;TEntity>|query <small style='border:solid 1px #aaa'>Expression<Func<TEntity,Boolean>></small><br/>queryId <small style='border:solid 1px #aaa'>Guid</small><br/>offset <small style='border:solid 1px #aaa'>Int32</small><br/>count <small style='border:solid 1px #aaa'>Nullable<Int32></small><br/>totalCount <small style='border:solid 1px #aaa'>Int32&</small><br/>overrideAuthContext <small style='border:solid 1px #aaa'>IPrincipal</small>|Queries or continues a query in lean mode|

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
	public IEnumerable<TEntity> QueryFast(Expression<Func<TEntity,Boolean>> query,Guid queryId,Int32 offset,Nullable<Int32> count,Int32& totalCount,IPrincipal overrideAuthContext){
		throw new System.NotImplementedException();
	}
}
```

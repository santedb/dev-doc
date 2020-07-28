---
description: IFastQueryDataPersistenceService`1 (SanteDB.Core.Api)
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
|QueryFast|System.Collections.Generic.IEnumerable&lt;TEntity>|query <small style='border:solid 1px #aaa'>System.Linq.Expressions.Expression<System.Func<TEntity,System.Boolean>></small><br/>queryId <small style='border:solid 1px #aaa'>System.Guid</small><br/>offset <small style='border:solid 1px #aaa'>System.Int32</small><br/>count <small style='border:solid 1px #aaa'>System.Nullable<System.Int32></small><br/>totalCount <small style='border:solid 1px #aaa'>System.Int32&</small><br/>overrideAuthContext <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Queries or continues a query in lean mode|

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

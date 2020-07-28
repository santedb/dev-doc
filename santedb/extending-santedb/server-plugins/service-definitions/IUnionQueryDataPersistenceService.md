---
description: IUnionQueryDataPersistenceService`1 (SanteDB.Core.Api)
---

## Summary
Represents a data persistence provider that can store and continue queries

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Union|System.Collections.Generic.IEnumerable&lt;TEntity>|queries <small style='border:solid 1px #aaa'></small><br/>queryId <small style='border:solid 1px #aaa'>System.Guid</small><br/>offset <small style='border:solid 1px #aaa'>System.Int32</small><br/>count <small style='border:solid 1px #aaa'>System.Nullable<System.Int32></small><br/>totalCount <small style='border:solid 1px #aaa'>System.Int32&</small><br/>overrideAuthContext <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small><br/>orderBy <small style='border:solid 1px #aaa'></small>|Queries or continues a query|

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyUnionQueryDataPersistenceService<TEntity> : SanteDB.Core.Services.IUnionQueryDataPersistenceService<TEntity> { 
	public String ServiceName => "My own IUnionQueryDataPersistenceService`1 service";
	/// <summary>
	/// Queries or continues a query
	/// </summary>
	public System.Collections.Generic.IEnumerable<TEntity> Union( queries,System.Guid queryId,System.Int32 offset,System.Nullable<System.Int32> count,System.Int32& totalCount,System.Security.Principal.IPrincipal overrideAuthContext, orderBy){
		throw new System.NotImplementedException();
	}
}
```

---
description: IUnionQueryDataPersistenceService<TEntity> (SanteDB.Core.Api)
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
|Union|IEnumerable&lt;TEntity>|queries <small style='border:solid 1px #aaa'>Expression`1[]</small><br/>queryId <small style='border:solid 1px #aaa'>Guid</small><br/>offset <small style='border:solid 1px #aaa'>Int32</small><br/>count <small style='border:solid 1px #aaa'>Nullable<Int32></small><br/>totalCount <small style='border:solid 1px #aaa'>Int32&</small><br/>overrideAuthContext <small style='border:solid 1px #aaa'>IPrincipal</small><br/>orderBy <small style='border:solid 1px #aaa'>ModelSort`1[]</small>|Queries or continues a query|

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
	public IEnumerable<TEntity> Union(Expression`1[] queries,Guid queryId,Int32 offset,Nullable<Int32> count,Int32& totalCount,IPrincipal overrideAuthContext,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
}
```

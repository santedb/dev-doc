---
description: IStoredQueryDataPersistenceService<TEntity> (SanteDB.Core.Api)
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
|Query|IEnumerable&lt;TEntity>|query <small style='border:solid 1px #aaa'>Expression<Func<TEntity,Boolean>></small><br/>queryId <small style='border:solid 1px #aaa'>Guid</small><br/>offset <small style='border:solid 1px #aaa'>Int32</small><br/>count <small style='border:solid 1px #aaa'>Nullable<Int32></small><br/>totalCount <small style='border:solid 1px #aaa'>Int32&</small><br/>overrideAuthContext <small style='border:solid 1px #aaa'>IPrincipal</small><br/>orderBy <small style='border:solid 1px #aaa'>ModelSort`1[]</small>|Queries or continues a query|

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyStoredQueryDataPersistenceService<TEntity> : SanteDB.Core.Services.IStoredQueryDataPersistenceService<TEntity> { 
	public String ServiceName => "My own IStoredQueryDataPersistenceService`1 service";
	/// <summary>
	/// Queries or continues a query
	/// </summary>
	public IEnumerable<TEntity> Query(Expression<Func<TEntity,Boolean>> query,Guid queryId,Int32 offset,Nullable<Int32> count,Int32& totalCount,IPrincipal overrideAuthContext,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
}
```

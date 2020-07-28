---
description: IPersistableQueryRepositoryService<TEntity> (SanteDB.Core.Api)
---

## Summary
Persistable query provider is an extensable interface which can perform a query with state

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Find|IEnumerable&lt;TEntity>|query <small style='border:solid 1px #aaa'>Expression<Func<TEntity,Boolean>></small><br/>offset <small style='border:solid 1px #aaa'>Int32</small><br/>count <small style='border:solid 1px #aaa'>Nullable<Int32></small><br/>totalResults <small style='border:solid 1px #aaa'>Int32&</small><br/>queryId <small style='border:solid 1px #aaa'>Guid</small><br/>orderBy <small style='border:solid 1px #aaa'>ModelSort`1[]</small>|Performs a query which|

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyPersistableQueryRepositoryService<TEntity> : SanteDB.Core.Services.IPersistableQueryRepositoryService<TEntity> { 
	public String ServiceName => "My own IPersistableQueryRepositoryService`1 service";
	/// <summary>
	/// Performs a query which
	/// </summary>
	public IEnumerable<TEntity> Find(Expression<Func<TEntity,Boolean>> query,Int32 offset,Nullable<Int32> count,Int32& totalResults,Guid queryId,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
}
```

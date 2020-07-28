---
description: IPersistableQueryRepositoryService`1 (SanteDB.Core.Api)
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
|Find|System.Collections.Generic.IEnumerable&lt;TEntity>|query <small style='border:solid 1px #aaa'>System.Linq.Expressions.Expression<System.Func<TEntity,System.Boolean>></small><br/>offset <small style='border:solid 1px #aaa'>System.Int32</small><br/>count <small style='border:solid 1px #aaa'>System.Nullable<System.Int32></small><br/>totalResults <small style='border:solid 1px #aaa'>System.Int32&</small><br/>queryId <small style='border:solid 1px #aaa'>System.Guid</small><br/>orderBy <small style='border:solid 1px #aaa'></small>|Performs a query which|

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
	public System.Collections.Generic.IEnumerable<TEntity> Find(System.Linq.Expressions.Expression<System.Func<TEntity,System.Boolean>> query,System.Int32 offset,System.Nullable<System.Int32> count,System.Int32& totalResults,System.Guid queryId, orderBy){
		throw new System.NotImplementedException();
	}
}
```

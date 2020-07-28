---
description: IRepositoryService<TModel> (SanteDB.Core.Api)
---

## Summary
Represents a repository service base

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Get|TModel|key <small style='border:solid 1px #aaa'>Guid</small>|Gets the specified model.|
|Get|TModel|key <small style='border:solid 1px #aaa'>Guid</small><br/>versionKey <small style='border:solid 1px #aaa'>Guid</small>|Gets the specified model.|
|Find|IEnumerable&lt;TModel>|query <small style='border:solid 1px #aaa'>Expression<Func<TModel,Boolean>></small>|Finds the specified data.|
|Find|IEnumerable&lt;TModel>|query <small style='border:solid 1px #aaa'>Expression<Func<TModel,Boolean>></small><br/>offset <small style='border:solid 1px #aaa'>Int32</small><br/>count <small style='border:solid 1px #aaa'>Nullable<Int32></small><br/>totalResults <small style='border:solid 1px #aaa'>Int32&</small><br/>orderBy <small style='border:solid 1px #aaa'>ModelSort`1[]</small>|Finds the specified data.|
|Insert|TModel|data <small style='border:solid 1px #aaa'>TModel</small>|Inserts the specified data.|
|Save|TModel|data <small style='border:solid 1px #aaa'>TModel</small>|Saves the specified data.|
|Obsolete|TModel|key <small style='border:solid 1px #aaa'>Guid</small>|Obsoletes the specified data.|

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyRepositoryService<TModel> : SanteDB.Core.Services.IRepositoryService<TModel> { 
	public String ServiceName => "My own IRepositoryService`1 service";
	/// <summary>
	/// Gets the specified model.
	/// </summary>
	public TModel Get(Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified model.
	/// </summary>
	public TModel Get(Guid key,Guid versionKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Finds the specified data.
	/// </summary>
	public IEnumerable<TModel> Find(Expression<Func<TModel,Boolean>> query){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Finds the specified data.
	/// </summary>
	public IEnumerable<TModel> Find(Expression<Func<TModel,Boolean>> query,Int32 offset,Nullable<Int32> count,Int32& totalResults,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Inserts the specified data.
	/// </summary>
	public TModel Insert(TModel data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Saves the specified data.
	/// </summary>
	public TModel Save(TModel data){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Obsoletes the specified data.
	/// </summary>
	public TModel Obsolete(Guid key){
		throw new System.NotImplementedException();
	}
}
```

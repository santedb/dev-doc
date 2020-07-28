---
description: IRepositoryService`1 (SanteDB.Core.Api)
---

## Summary
Represents a repository service base

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
	public TModel Get(System.Guid key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified model.
	/// </summary>
	public TModel Get(System.Guid key,System.Guid versionKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Finds the specified data.
	/// </summary>
	public System.Collections.Generic.IEnumerable<TModel> Find(System.Linq.Expressions.Expression<System.Func<TModel,System.Boolean>> query){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Finds the specified data.
	/// </summary>
	public System.Collections.Generic.IEnumerable<TModel> Find(System.Linq.Expressions.Expression<System.Func<TModel,System.Boolean>> query,System.Int32 offset,System.Nullable<System.Int32> count,System.Int32& totalResults, orderBy){
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
	public TModel Obsolete(System.Guid key){
		throw new System.NotImplementedException();
	}
}
```

---
description: IRepositoryService<TModel> (SanteDB.Core.Api)
---

## Summary
Represents a repository service base

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Get|TModel|*Guid* **key**|Gets the specified model.|
|Get|TModel|*Guid* **key**<br/>*Guid* **versionKey**|Gets the specified model.|
|Find|IEnumerable&lt;TModel>|*Expression&lt;Func&lt;TModel,Boolean>>* **query**|Finds the specified data.|
|Find|IEnumerable&lt;TModel>|*Expression&lt;Func&lt;TModel,Boolean>>* **query**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**<br/>*ModelSort`1[]* **orderBy**|Finds the specified data.|
|Insert|TModel|*TModel* **data**|Inserts the specified data.|
|Save|TModel|*TModel* **data**|Saves the specified data.|
|Obsolete|TModel|*Guid* **key**|Obsoletes the specified data.|

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

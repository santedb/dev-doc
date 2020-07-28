---
description: IDataPersistenceService<TData> (SanteDB.Core.Api)
---

## Summary
Represents a data persistence service which is capable of storing and retrieving data
            to/from a data store

## Events

|Event|Type|Description|
|-|-|-|
|Inserted|EventHandler&lt;DataPersistedEventArgs&lt;TData>>|Occurs when inserted.|
|Inserting|EventHandler&lt;DataPersistingEventArgs&lt;TData>>|Occurs when inserting.|
|Updated|EventHandler&lt;DataPersistedEventArgs&lt;TData>>|Occurs when updated.|
|Updating|EventHandler&lt;DataPersistingEventArgs&lt;TData>>|Occurs when updating.|
|Obsoleted|EventHandler&lt;DataPersistedEventArgs&lt;TData>>|Occurs when obsoleted.|
|Obsoleting|EventHandler&lt;DataPersistingEventArgs&lt;TData>>|Occurs when obsoleting.|
|Queried|EventHandler&lt;QueryResultEventArgs&lt;TData>>|Occurs when queried.|
|Querying|EventHandler&lt;QueryRequestEventArgs&lt;TData>>|Occurs when querying.|
|Retrieving|EventHandler&lt;DataRetrievingEventArgs&lt;TData>>|Data is being retrieved|
|Retrieved|EventHandler&lt;DataRetrievedEventArgs&lt;TData>>|Fired when data has been retrieved|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Insert|TData|data <small style='border:solid 1px #aaa'>TData</small><br/>mode <small style='border:solid 1px #aaa'>TransactionMode</small><br/>principal <small style='border:solid 1px #aaa'>IPrincipal</small>|Insert the specified data.|
|Update|TData|data <small style='border:solid 1px #aaa'>TData</small><br/>mode <small style='border:solid 1px #aaa'>TransactionMode</small><br/>principal <small style='border:solid 1px #aaa'>IPrincipal</small>|Update the specified data|
|Obsolete|TData|data <small style='border:solid 1px #aaa'>TData</small><br/>mode <small style='border:solid 1px #aaa'>TransactionMode</small><br/>principal <small style='border:solid 1px #aaa'>IPrincipal</small>|Obsolete the specified identified data|
|Get|TData|key <small style='border:solid 1px #aaa'>Guid</small><br/>versionKey <small style='border:solid 1px #aaa'>Nullable<Guid></small><br/>loadFast <small style='border:solid 1px #aaa'>Boolean</small><br/>principal <small style='border:solid 1px #aaa'>IPrincipal</small>|Get the specified key.|
|Query|IEnumerable&lt;TData>|query <small style='border:solid 1px #aaa'>Expression<Func<TData,Boolean>></small><br/>principal <small style='border:solid 1px #aaa'>IPrincipal</small>|Query the specified data|
|Query|IEnumerable&lt;TData>|query <small style='border:solid 1px #aaa'>Expression<Func<TData,Boolean>></small><br/>offset <small style='border:solid 1px #aaa'>Int32</small><br/>count <small style='border:solid 1px #aaa'>Nullable<Int32></small><br/>totalResults <small style='border:solid 1px #aaa'>Int32&</small><br/>principal <small style='border:solid 1px #aaa'>IPrincipal</small><br/>orderBy <small style='border:solid 1px #aaa'>ModelSort`1[]</small>|Query the specified data|
|Count|Int64|p <small style='border:solid 1px #aaa'>Expression<Func<TData,Boolean>></small><br/>authContext <small style='border:solid 1px #aaa'>IPrincipal</small>|Performs a fast count|

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyDataPersistenceService<TData> : SanteDB.Core.Services.IDataPersistenceService<TData> { 
	public String ServiceName => "My own IDataPersistenceService`1 service";
	/// <summary>
	/// Occurs when inserted.
	/// </summary>
	public event EventHandler<DataPersistedEventArgs<TData>> Inserted;
	/// <summary>
	/// Occurs when inserting.
	/// </summary>
	public event EventHandler<DataPersistingEventArgs<TData>> Inserting;
	/// <summary>
	/// Occurs when updated.
	/// </summary>
	public event EventHandler<DataPersistedEventArgs<TData>> Updated;
	/// <summary>
	/// Occurs when updating.
	/// </summary>
	public event EventHandler<DataPersistingEventArgs<TData>> Updating;
	/// <summary>
	/// Occurs when obsoleted.
	/// </summary>
	public event EventHandler<DataPersistedEventArgs<TData>> Obsoleted;
	/// <summary>
	/// Occurs when obsoleting.
	/// </summary>
	public event EventHandler<DataPersistingEventArgs<TData>> Obsoleting;
	/// <summary>
	/// Occurs when queried.
	/// </summary>
	public event EventHandler<QueryResultEventArgs<TData>> Queried;
	/// <summary>
	/// Occurs when querying.
	/// </summary>
	public event EventHandler<QueryRequestEventArgs<TData>> Querying;
	/// <summary>
	/// Data is being retrieved
	/// </summary>
	public event EventHandler<DataRetrievingEventArgs<TData>> Retrieving;
	/// <summary>
	/// Fired when data has been retrieved
	/// </summary>
	public event EventHandler<DataRetrievedEventArgs<TData>> Retrieved;
	/// <summary>
	/// Insert the specified data.
	/// </summary>
	public TData Insert(TData data,TransactionMode mode,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Update the specified data
	/// </summary>
	public TData Update(TData data,TransactionMode mode,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Obsolete the specified identified data
	/// </summary>
	public TData Obsolete(TData data,TransactionMode mode,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the specified key.
	/// </summary>
	public TData Get(Guid key,Nullable<Guid> versionKey,Boolean loadFast,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Query the specified data
	/// </summary>
	public IEnumerable<TData> Query(Expression<Func<TData,Boolean>> query,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Query the specified data
	/// </summary>
	public IEnumerable<TData> Query(Expression<Func<TData,Boolean>> query,Int32 offset,Nullable<Int32> count,Int32& totalResults,IPrincipal principal,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Performs a fast count
	/// </summary>
	public Int64 Count(Expression<Func<TData,Boolean>> p,IPrincipal authContext){
		throw new System.NotImplementedException();
	}
}
```

---
description: IDataPersistenceService`1 (SanteDB.Core.Api)
---

## Summary
Represents a data persistence service which is capable of storing and retrieving data
            to/from a data store

## Events

|Event|Type|Description|
|-|-|-|
|Inserted|System.EventHandler&lt;SanteDB.Core.Event.DataPersistedEventArgs&lt;TData>>|Occurs when inserted.|
|Inserting|System.EventHandler&lt;SanteDB.Core.Event.DataPersistingEventArgs&lt;TData>>|Occurs when inserting.|
|Updated|System.EventHandler&lt;SanteDB.Core.Event.DataPersistedEventArgs&lt;TData>>|Occurs when updated.|
|Updating|System.EventHandler&lt;SanteDB.Core.Event.DataPersistingEventArgs&lt;TData>>|Occurs when updating.|
|Obsoleted|System.EventHandler&lt;SanteDB.Core.Event.DataPersistedEventArgs&lt;TData>>|Occurs when obsoleted.|
|Obsoleting|System.EventHandler&lt;SanteDB.Core.Event.DataPersistingEventArgs&lt;TData>>|Occurs when obsoleting.|
|Queried|System.EventHandler&lt;SanteDB.Core.Event.QueryResultEventArgs&lt;TData>>|Occurs when queried.|
|Querying|System.EventHandler&lt;SanteDB.Core.Event.QueryRequestEventArgs&lt;TData>>|Occurs when querying.|
|Retrieving|System.EventHandler&lt;SanteDB.Core.Event.DataRetrievingEventArgs&lt;TData>>|Data is being retrieved|
|Retrieved|System.EventHandler&lt;SanteDB.Core.Event.DataRetrievedEventArgs&lt;TData>>|Fired when data has been retrieved|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Insert|TData|data <small style='border:solid 1px #aaa'>TData</small><br/>mode <small style='border:solid 1px #aaa'>SanteDB.Core.Services.TransactionMode</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Insert the specified data.|
|Update|TData|data <small style='border:solid 1px #aaa'>TData</small><br/>mode <small style='border:solid 1px #aaa'>SanteDB.Core.Services.TransactionMode</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Update the specified data|
|Obsolete|TData|data <small style='border:solid 1px #aaa'>TData</small><br/>mode <small style='border:solid 1px #aaa'>SanteDB.Core.Services.TransactionMode</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Obsolete the specified identified data|
|Get|TData|key <small style='border:solid 1px #aaa'>System.Guid</small><br/>versionKey <small style='border:solid 1px #aaa'>System.Nullable<System.Guid></small><br/>loadFast <small style='border:solid 1px #aaa'>System.Boolean</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Get the specified key.|
|Query|System.Collections.Generic.IEnumerable&lt;TData>|query <small style='border:solid 1px #aaa'>System.Linq.Expressions.Expression<System.Func<TData,System.Boolean>></small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Query the specified data|
|Query|System.Collections.Generic.IEnumerable&lt;TData>|query <small style='border:solid 1px #aaa'>System.Linq.Expressions.Expression<System.Func<TData,System.Boolean>></small><br/>offset <small style='border:solid 1px #aaa'>System.Int32</small><br/>count <small style='border:solid 1px #aaa'>System.Nullable<System.Int32></small><br/>totalResults <small style='border:solid 1px #aaa'>System.Int32&</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small><br/>orderBy <small style='border:solid 1px #aaa'></small>|Query the specified data|
|Count|System.Int64|p <small style='border:solid 1px #aaa'>System.Linq.Expressions.Expression<System.Func<TData,System.Boolean>></small><br/>authContext <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Performs a fast count|

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
	public event System.EventHandler<SanteDB.Core.Event.DataPersistedEventArgs<TData>> Inserted;
	/// <summary>
	/// Occurs when inserting.
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataPersistingEventArgs<TData>> Inserting;
	/// <summary>
	/// Occurs when updated.
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataPersistedEventArgs<TData>> Updated;
	/// <summary>
	/// Occurs when updating.
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataPersistingEventArgs<TData>> Updating;
	/// <summary>
	/// Occurs when obsoleted.
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataPersistedEventArgs<TData>> Obsoleted;
	/// <summary>
	/// Occurs when obsoleting.
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataPersistingEventArgs<TData>> Obsoleting;
	/// <summary>
	/// Occurs when queried.
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.QueryResultEventArgs<TData>> Queried;
	/// <summary>
	/// Occurs when querying.
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.QueryRequestEventArgs<TData>> Querying;
	/// <summary>
	/// Data is being retrieved
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataRetrievingEventArgs<TData>> Retrieving;
	/// <summary>
	/// Fired when data has been retrieved
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataRetrievedEventArgs<TData>> Retrieved;
	/// <summary>
	/// Insert the specified data.
	/// </summary>
	public TData Insert(TData data,SanteDB.Core.Services.TransactionMode mode,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Update the specified data
	/// </summary>
	public TData Update(TData data,SanteDB.Core.Services.TransactionMode mode,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Obsolete the specified identified data
	/// </summary>
	public TData Obsolete(TData data,SanteDB.Core.Services.TransactionMode mode,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the specified key.
	/// </summary>
	public TData Get(System.Guid key,System.Nullable<System.Guid> versionKey,System.Boolean loadFast,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Query the specified data
	/// </summary>
	public System.Collections.Generic.IEnumerable<TData> Query(System.Linq.Expressions.Expression<System.Func<TData,System.Boolean>> query,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Query the specified data
	/// </summary>
	public System.Collections.Generic.IEnumerable<TData> Query(System.Linq.Expressions.Expression<System.Func<TData,System.Boolean>> query,System.Int32 offset,System.Nullable<System.Int32> count,System.Int32& totalResults,System.Security.Principal.IPrincipal principal, orderBy){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Performs a fast count
	/// </summary>
	public System.Int64 Count(System.Linq.Expressions.Expression<System.Func<TData,System.Boolean>> p,System.Security.Principal.IPrincipal authContext){
		throw new System.NotImplementedException();
	}
}
```

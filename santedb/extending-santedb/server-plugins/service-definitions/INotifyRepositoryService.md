---
description: INotifyRepositoryService`1 (SanteDB.Core.Api)
---

## Summary
Repreents a repository which notifies of changes

## Events

|Event|Type|Description|
|-|-|-|
|Inserting|System.EventHandler&lt;SanteDB.Core.Event.DataPersistingEventArgs&lt;TModel>>|Data is inserting|
|Inserted|System.EventHandler&lt;SanteDB.Core.Event.DataPersistedEventArgs&lt;TModel>>|Fired after data was inserted|
|Saving|System.EventHandler&lt;SanteDB.Core.Event.DataPersistingEventArgs&lt;TModel>>|Fired before saving|
|Saved|System.EventHandler&lt;SanteDB.Core.Event.DataPersistedEventArgs&lt;TModel>>|Fired after data was saved|
|Obsoleting|System.EventHandler&lt;SanteDB.Core.Event.DataPersistingEventArgs&lt;TModel>>|Fired before obsoleting|
|Obsoleted|System.EventHandler&lt;SanteDB.Core.Event.DataPersistedEventArgs&lt;TModel>>|Fired after data was obsoleted|
|Retrieving|System.EventHandler&lt;SanteDB.Core.Event.DataRetrievingEventArgs&lt;TModel>>|Retrieving the data|
|Retrieved|System.EventHandler&lt;SanteDB.Core.Event.DataRetrievedEventArgs&lt;TModel>>|Fired after data was retrieved|
|Querying|System.EventHandler&lt;SanteDB.Core.Event.QueryRequestEventArgs&lt;TModel>>|Fired after data was queried|
|Queried|System.EventHandler&lt;SanteDB.Core.Event.QueryResultEventArgs&lt;TModel>>|Fired after data was queried|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|

## Implementations

None

## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyNotifyRepositoryService<TModel> : SanteDB.Core.Services.INotifyRepositoryService<TModel> { 
	public String ServiceName => "My own INotifyRepositoryService`1 service";
	/// <summary>
	/// Data is inserting
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataPersistingEventArgs<TModel>> Inserting;
	/// <summary>
	/// Fired after data was inserted
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataPersistedEventArgs<TModel>> Inserted;
	/// <summary>
	/// Fired before saving
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataPersistingEventArgs<TModel>> Saving;
	/// <summary>
	/// Fired after data was saved
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataPersistedEventArgs<TModel>> Saved;
	/// <summary>
	/// Fired before obsoleting
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataPersistingEventArgs<TModel>> Obsoleting;
	/// <summary>
	/// Fired after data was obsoleted
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataPersistedEventArgs<TModel>> Obsoleted;
	/// <summary>
	/// Retrieving the data
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataRetrievingEventArgs<TModel>> Retrieving;
	/// <summary>
	/// Fired after data was retrieved
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.DataRetrievedEventArgs<TModel>> Retrieved;
	/// <summary>
	/// Fired after data was queried
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.QueryRequestEventArgs<TModel>> Querying;
	/// <summary>
	/// Fired after data was queried
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Event.QueryResultEventArgs<TModel>> Queried;
}
```

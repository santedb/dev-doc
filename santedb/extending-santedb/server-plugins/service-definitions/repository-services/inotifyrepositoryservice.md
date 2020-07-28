---
description: INotifyRepositoryService<TModel> (SanteDB.Core.Api)
---

# Notifiable Repository Service

## Summary

Repreents a repository which notifies of changes

## Events

| Event | Type | Description |
| :--- | :--- | :--- |
| Inserting | EventHandler&lt;DataPersistingEventArgs&lt;TModel&gt;&gt; | Data is inserting |
| Inserted | EventHandler&lt;DataPersistedEventArgs&lt;TModel&gt;&gt; | Fired after data was inserted |
| Saving | EventHandler&lt;DataPersistingEventArgs&lt;TModel&gt;&gt; | Fired before saving |
| Saved | EventHandler&lt;DataPersistedEventArgs&lt;TModel&gt;&gt; | Fired after data was saved |
| Obsoleting | EventHandler&lt;DataPersistingEventArgs&lt;TModel&gt;&gt; | Fired before obsoleting |
| Obsoleted | EventHandler&lt;DataPersistedEventArgs&lt;TModel&gt;&gt; | Fired after data was obsoleted |
| Retrieving | EventHandler&lt;DataRetrievingEventArgs&lt;TModel&gt;&gt; | Retrieving the data |
| Retrieved | EventHandler&lt;DataRetrievedEventArgs&lt;TModel&gt;&gt; | Fired after data was retrieved |
| Querying | EventHandler&lt;QueryRequestEventArgs&lt;TModel&gt;&gt; | Fired after data was queried |
| Queried | EventHandler&lt;QueryResultEventArgs&lt;TModel&gt;&gt; | Fired after data was queried |

## Implementations

None

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyNotifyRepositoryService<TModel> : SanteDB.Core.Services.INotifyRepositoryService<TModel> { 
    public String ServiceName => "My own INotifyRepositoryService`1 service";
    /// <summary>
    /// Data is inserting
    /// </summary>
    public event EventHandler<DataPersistingEventArgs<TModel>> Inserting;
    /// <summary>
    /// Fired after data was inserted
    /// </summary>
    public event EventHandler<DataPersistedEventArgs<TModel>> Inserted;
    /// <summary>
    /// Fired before saving
    /// </summary>
    public event EventHandler<DataPersistingEventArgs<TModel>> Saving;
    /// <summary>
    /// Fired after data was saved
    /// </summary>
    public event EventHandler<DataPersistedEventArgs<TModel>> Saved;
    /// <summary>
    /// Fired before obsoleting
    /// </summary>
    public event EventHandler<DataPersistingEventArgs<TModel>> Obsoleting;
    /// <summary>
    /// Fired after data was obsoleted
    /// </summary>
    public event EventHandler<DataPersistedEventArgs<TModel>> Obsoleted;
    /// <summary>
    /// Retrieving the data
    /// </summary>
    public event EventHandler<DataRetrievingEventArgs<TModel>> Retrieving;
    /// <summary>
    /// Fired after data was retrieved
    /// </summary>
    public event EventHandler<DataRetrievedEventArgs<TModel>> Retrieved;
    /// <summary>
    /// Fired after data was queried
    /// </summary>
    public event EventHandler<QueryRequestEventArgs<TModel>> Querying;
    /// <summary>
    /// Fired after data was queried
    /// </summary>
    public event EventHandler<QueryResultEventArgs<TModel>> Queried;
}
```


---
description: INotifyRepositoryService<TModel> (SanteDB.Core.Api)
---

# Notifiable Repository Service

## Summary

Repreents a repository which notifies of changes

## Events

| Event      | Type                                            | Description                    |
| ---------- | ----------------------------------------------- | ------------------------------ |
| Inserting  | EventHandler\<DataPersistingEventArgs\<TModel>> | Data is inserting              |
| Inserted   | EventHandler\<DataPersistedEventArgs\<TModel>>  | Fired after data was inserted  |
| Saving     | EventHandler\<DataPersistingEventArgs\<TModel>> | Fired before saving            |
| Saved      | EventHandler\<DataPersistedEventArgs\<TModel>>  | Fired after data was saved     |
| Obsoleting | EventHandler\<DataPersistingEventArgs\<TModel>> | Fired before obsoleting        |
| Obsoleted  | EventHandler\<DataPersistedEventArgs\<TModel>>  | Fired after data was obsoleted |
| Retrieving | EventHandler\<DataRetrievingEventArgs\<TModel>> | Retrieving the data            |
| Retrieved  | EventHandler\<DataRetrievedEventArgs\<TModel>>  | Fired after data was retrieved |
| Querying   | EventHandler\<QueryRequestEventArgs\<TModel>>   | Fired after data was queried   |
| Queried    | EventHandler\<QueryResultEventArgs\<TModel>>    | Fired after data was queried   |

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

---
description: IDataPersistenceService<TData> (SanteDB.Core.Api)
---

# Data Persistence Service

## Summary

Represents a data persistence service which is capable of storing and retrieving data to/from a data store

## Events

| Event      | Type                                           | Description                        |
| ---------- | ---------------------------------------------- | ---------------------------------- |
| Inserted   | EventHandler\<DataPersistedEventArgs\<TData>>  | Occurs when inserted.              |
| Inserting  | EventHandler\<DataPersistingEventArgs\<TData>> | Occurs when inserting.             |
| Updated    | EventHandler\<DataPersistedEventArgs\<TData>>  | Occurs when updated.               |
| Updating   | EventHandler\<DataPersistingEventArgs\<TData>> | Occurs when updating.              |
| Obsoleted  | EventHandler\<DataPersistedEventArgs\<TData>>  | Occurs when obsoleted.             |
| Obsoleting | EventHandler\<DataPersistingEventArgs\<TData>> | Occurs when obsoleting.            |
| Queried    | EventHandler\<QueryResultEventArgs\<TData>>    | Occurs when queried.               |
| Querying   | EventHandler\<QueryRequestEventArgs\<TData>>   | Occurs when querying.              |
| Retrieving | EventHandler\<DataRetrievingEventArgs\<TData>> | Data is being retrieved            |
| Retrieved  | EventHandler\<DataRetrievedEventArgs\<TData>>  | Fired when data has been retrieved |

## Operations

| Operation | Response/Return     | Input/Parameter                                                                                                                                                                                                                                                                                                                               | Description                            |
| --------- | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- |
| Insert    | TData               | <p><em>TData</em> <strong>data</strong><br><em>TransactionMode</em> <strong>mode</strong><br><em>IPrincipal</em> <strong>principal</strong></p>                                                                                                                                                                                               | Insert the specified data.             |
| Update    | TData               | <p><em>TData</em> <strong>data</strong><br><em>TransactionMode</em> <strong>mode</strong><br><em>IPrincipal</em> <strong>principal</strong></p>                                                                                                                                                                                               | Update the specified data              |
| Obsolete  | TData               | <p><em>TData</em> <strong>data</strong><br><em>TransactionMode</em> <strong>mode</strong><br><em>IPrincipal</em> <strong>principal</strong></p>                                                                                                                                                                                               | Obsolete the specified identified data |
| Get       | TData               | <p><em>Guid</em> <strong>key</strong><br><em>Nullable&#x3C;Guid></em> <strong>versionKey</strong><br><em>Boolean</em> <strong>loadFast</strong><br><em>IPrincipal</em> <strong>principal</strong></p>                                                                                                                                         | Get the specified key.                 |
| Query     | IEnumerable\<TData> | <p><em>Expression&#x3C;Func&#x3C;TData,Boolean>></em> <strong>query</strong><br><em>IPrincipal</em> <strong>principal</strong></p>                                                                                                                                                                                                            | Query the specified data               |
| Query     | IEnumerable\<TData> | <p><em>Expression&#x3C;Func&#x3C;TData,Boolean>></em> <strong>query</strong><br><em>Int32</em> <strong>offset</strong><br><em>Nullable&#x3C;Int32></em> <strong>count</strong><br><em>Int32&#x26;</em> <strong>totalResults</strong><br><em>IPrincipal</em> <strong>principal</strong><br><em>ModelSort`1[]</em> <strong>orderBy</strong></p> | Query the specified data               |
| Count     | Int64               | <p><em>Expression&#x3C;Func&#x3C;TData,Boolean>></em> <strong>p</strong><br><em>IPrincipal</em> <strong>authContext</strong></p>                                                                                                                                                                                                              | Performs a fast count                  |

## Implementations

None

## Example Implementation

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

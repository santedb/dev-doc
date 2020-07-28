---
description: IDataPersistenceService<TData> (SanteDB.Core.Api)
---

# Data Persistence Service

## Summary

Represents a data persistence service which is capable of storing and retrieving data to/from a data store

## Events

| Event | Type | Description |
| :--- | :--- | :--- |
| Inserted | EventHandler&lt;DataPersistedEventArgs&lt;TData&gt;&gt; | Occurs when inserted. |
| Inserting | EventHandler&lt;DataPersistingEventArgs&lt;TData&gt;&gt; | Occurs when inserting. |
| Updated | EventHandler&lt;DataPersistedEventArgs&lt;TData&gt;&gt; | Occurs when updated. |
| Updating | EventHandler&lt;DataPersistingEventArgs&lt;TData&gt;&gt; | Occurs when updating. |
| Obsoleted | EventHandler&lt;DataPersistedEventArgs&lt;TData&gt;&gt; | Occurs when obsoleted. |
| Obsoleting | EventHandler&lt;DataPersistingEventArgs&lt;TData&gt;&gt; | Occurs when obsoleting. |
| Queried | EventHandler&lt;QueryResultEventArgs&lt;TData&gt;&gt; | Occurs when queried. |
| Querying | EventHandler&lt;QueryRequestEventArgs&lt;TData&gt;&gt; | Occurs when querying. |
| Retrieving | EventHandler&lt;DataRetrievingEventArgs&lt;TData&gt;&gt; | Data is being retrieved |
| Retrieved | EventHandler&lt;DataRetrievedEventArgs&lt;TData&gt;&gt; | Fired when data has been retrieved |

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| Insert | TData | _TData_ **data** _TransactionMode_ **mode** _IPrincipal_ **principal** | Insert the specified data. |
| Update | TData | _TData_ **data** _TransactionMode_ **mode** _IPrincipal_ **principal** | Update the specified data |
| Obsolete | TData | _TData_ **data** _TransactionMode_ **mode** _IPrincipal_ **principal** | Obsolete the specified identified data |
| Get | TData | _Guid_ **key** _Nullable&lt;Guid&gt;_ **versionKey** _Boolean_ **loadFast** _IPrincipal_ **principal** | Get the specified key. |
| Query | IEnumerable&lt;TData&gt; | _Expression&lt;Func&lt;TData,Boolean&gt;&gt;_ **query** _IPrincipal_ **principal** | Query the specified data |
| Query | IEnumerable&lt;TData&gt; | _Expression&lt;Func&lt;TData,Boolean&gt;&gt;_ **query** _Int32_ **offset** _Nullable&lt;Int32&gt;_ **count** _Int32&_ **totalResults** _IPrincipal_ **principal** _ModelSort\`1\[\]_ **orderBy** | Query the specified data |
| Count | Int64 | _Expression&lt;Func&lt;TData,Boolean&gt;&gt;_ **p** _IPrincipal_ **authContext** | Performs a fast count |

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


---
description: IQueryPersistenceService (SanteDB.Core.Api)
---

# Query Persistence Service

## Summary

Query persistence service

## Operations

| Operation                | Response/Return    | Input/Parameter                                                                                                                                                                                   | Description                                                |
| ------------------------ | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| FindQueryId              | Guid               | _Object_ **queryTag**                                                                                                                                                                             | Find the query ID by the query tag                         |
| RegisterQuerySet         | Boolean            | <p><em>Guid</em> <strong>queryId</strong><br><em>IEnumerable&#x3C;Guid></em> <strong>results</strong><br><em>Object</em> <strong>tag</strong><br><em>Int32</em> <strong>totalResults</strong></p> | Register a query set                                       |
| IsRegistered             | Boolean            | _Guid_ **queryId**                                                                                                                                                                                | Returns true if the query identifier is already registered |
| GetQueryResults          | IEnumerable\<Guid> | <p><em>Guid</em> <strong>queryId</strong><br><em>Int32</em> <strong>offset</strong><br><em>Int32</em> <strong>count</strong></p>                                                                  | Get query results from the query set result store          |
| GetQueryTag              | Object             | _Guid_ **queryId**                                                                                                                                                                                | Get the query tag value from the result store              |
| QueryResultTotalQuantity | Int64              | _Guid_ **queryId**                                                                                                                                                                                | Count the number of remaining query results                |
| AddResults               | void               | <p><em>Guid</em> <strong>queryId</strong><br><em>IEnumerable&#x3C;Guid></em> <strong>results</strong></p>                                                                                         | Add results to the query                                   |
| SetQueryTag              | void               | <p><em>Guid</em> <strong>queryId</strong><br><em>Object</em> <strong>value</strong></p>                                                                                                           | Set or update the query tag of an existing query id        |

## Implementations

### Memory-Based Query Persistence Service - (SanteDB.Caching.Memory)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Caching.Memory.MemoryQueryPersistenceService, SanteDB.Caching.Memory, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

### REDIS Query Persistence Service - (SanteDB.Caching.Redis)

TODO: Document this

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Caching.Redis.RedisQueryPersistenceService, SanteDB.Caching.Redis, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyQueryPersistenceService : SanteDB.Core.Services.IQueryPersistenceService { 
    public String ServiceName => "My own IQueryPersistenceService service";
    /// <summary>
    /// Find the query ID by the query tag
    /// </summary>
    public Guid FindQueryId(Object queryTag){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Register a query set
    /// </summary>
    public Boolean RegisterQuerySet(Guid queryId,IEnumerable<Guid> results,Object tag,Int32 totalResults){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Returns true if the query identifier is already registered
    /// </summary>
    public Boolean IsRegistered(Guid queryId){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Get query results from the query set result store
    /// </summary>
    public IEnumerable<Guid> GetQueryResults(Guid queryId,Int32 offset,Int32 count){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Get the query tag value from the result store
    /// </summary>
    public Object GetQueryTag(Guid queryId){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Count the number of remaining query results
    /// </summary>
    public Int64 QueryResultTotalQuantity(Guid queryId){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Add results to the query
    /// </summary>
    public void AddResults(Guid queryId,IEnumerable<Guid> results){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Set or update the query tag of an existing query id
    /// </summary>
    public void SetQueryTag(Guid queryId,Object value){
        throw new System.NotImplementedException();
    }
}
```

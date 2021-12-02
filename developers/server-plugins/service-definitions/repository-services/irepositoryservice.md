---
description: IRepositoryService<TModel> (SanteDB.Core.Api)
---

# Generic Repository Service

## Summary

Represents a repository service base

## Operations

| Operation | Response/Return      | Input/Parameter                                                                                                                                                                                                                                                                              | Description                   |
| --------- | -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| Get       | TModel               | _Guid_ **key**                                                                                                                                                                                                                                                                               | Gets the specified model.     |
| Get       | TModel               | <p><em>Guid</em> <strong>key</strong><br><em>Guid</em> <strong>versionKey</strong></p>                                                                                                                                                                                                       | Gets the specified model.     |
| Find      | IEnumerable\<TModel> | _Expression\<Func\<TModel,Boolean>>_ **query**                                                                                                                                                                                                                                               | Finds the specified data.     |
| Find      | IEnumerable\<TModel> | <p><em>Expression&#x3C;Func&#x3C;TModel,Boolean>></em> <strong>query</strong><br><em>Int32</em> <strong>offset</strong><br><em>Nullable&#x3C;Int32></em> <strong>count</strong><br><em>Int32&#x26;</em> <strong>totalResults</strong><br><em>ModelSort`1[]</em> <strong>orderBy</strong></p> | Finds the specified data.     |
| Insert    | TModel               | _TModel_ **data**                                                                                                                                                                                                                                                                            | Inserts the specified data.   |
| Save      | TModel               | _TModel_ **data**                                                                                                                                                                                                                                                                            | Saves the specified data.     |
| Obsolete  | TModel               | _Guid_ **key**                                                                                                                                                                                                                                                                               | Obsoletes the specified data. |

## Implementations

None

## Example Implementation

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

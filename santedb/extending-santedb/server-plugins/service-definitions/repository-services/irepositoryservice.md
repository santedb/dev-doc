---
description: IRepositoryService<TModel> (SanteDB.Core.Api)
---

# Generic Repository Service

## Summary

Represents a repository service base

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| Get | TModel | _Guid_ **key** | Gets the specified model. |
| Get | TModel | _Guid_ **key** _Guid_ **versionKey** | Gets the specified model. |
| Find | IEnumerable&lt;TModel&gt; | _Expression&lt;Func&lt;TModel,Boolean&gt;&gt;_ **query** | Finds the specified data. |
| Find | IEnumerable&lt;TModel&gt; | _Expression&lt;Func&lt;TModel,Boolean&gt;&gt;_ **query** _Int32_ **offset** _Nullable&lt;Int32&gt;_ **count** _Int32&_ **totalResults** _ModelSort\`1\[\]_ **orderBy** | Finds the specified data. |
| Insert | TModel | _TModel_ **data** | Inserts the specified data. |
| Save | TModel | _TModel_ **data** | Saves the specified data. |
| Obsolete | TModel | _Guid_ **key** | Obsoletes the specified data. |

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


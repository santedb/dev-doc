---
description: IFreetextSearchService (SanteDB.Core.Api)
---

# Freetext Search Service

## Summary

Free text search service

## Operations

| Operation | Response/Return       | Input/Parameter                                                                                                                                                                                                                                           | Description            |
| --------- | --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| Search    | IEnumerable\<TEntity> | <p><em>String[]</em> <strong>term</strong><br><em>Int32</em> <strong>offset</strong><br><em>Nullable&#x3C;Int32></em> <strong>count</strong><br><em>Int32&#x26;</em> <strong>totalResults</strong><br><em>ModelSort`1[]</em> <strong>orderBy</strong></p> | Search based on tokens |

## Implementations

None

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyFreetextSearchService : SanteDB.Core.Services.IFreetextSearchService { 
    public String ServiceName => "My own IFreetextSearchService service";
    /// <summary>
    /// Search based on tokens
    /// </summary>
    public IEnumerable<TEntity> Search<TEntity>(String[] term,Int32 offset,Nullable<Int32> count,Int32& totalResults,ModelSort`1[] orderBy){
        throw new System.NotImplementedException();
    }
}
```

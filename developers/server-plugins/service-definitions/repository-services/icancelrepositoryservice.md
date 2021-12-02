---
description: ICancelRepositoryService<TModel> (SanteDB.Core.Api)
---

# Cancellable Repository

## Summary

Represents a repository that can cancel an act

## Operations

| Operation | Response/Return | Input/Parameter | Description                  |
| --------- | --------------- | --------------- | ---------------------------- |
| Cancel    | TModel          | _Guid_ **id**   | Cancels the specified object |

## Implementations

None

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyCancelRepositoryService<TModel> : SanteDB.Core.Services.ICancelRepositoryService<TModel> { 
    public String ServiceName => "My own ICancelRepositoryService`1 service";
    /// <summary>
    /// Cancels the specified object
    /// </summary>
    public TModel Cancel(Guid id){
        throw new System.NotImplementedException();
    }
}
```

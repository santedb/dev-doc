---
description: IStockManagementRepositoryService (SanteDB.Core.Api)
---

# Stock Management Repository

## Summary

Represents a stock management repository service.

## Operations

| Operation       | Response/Return                | Input/Parameter                                                                                                                                                                                                                                      | Description                                                          |
| --------------- | ------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Adjust          | Act                            | <p><em>ManufacturedMaterial</em> <strong>manufacturedMaterial</strong><br><em>Place</em> <strong>place</strong><br><em>Int32</em> <strong>quantity</strong><br><em>Concept</em> <strong>reason</strong></p>                                          | Performs a stock adjustment for the specified facility and material. |
| GetBalance      | Int32                          | <p><em>Place</em> <strong>place</strong><br><em>ManufacturedMaterial</em> <strong>manufacturedMaterial</strong></p>                                                                                                                                  | Gets the balance for the material.                                   |
| GetConsumed     | IEnumerable\<ActParticipation> | <p><em>Guid</em> <strong>manufacturedMaterialKey</strong><br><em>Guid</em> <strong>placeKey</strong><br><em>Nullable&#x3C;DateTimeOffset></em> <strong>startPeriod</strong><br><em>Nullable&#x3C;DateTimeOffset></em> <strong>endPeriod</strong></p> | Get the total amount of consumed objects                             |
| FindAdjustments | IEnumerable\<Act>              | <p><em>Guid</em> <strong>manufacturedMaterialKey</strong><br><em>Guid</em> <strong>placeKey</strong><br><em>Nullable&#x3C;DateTimeOffset></em> <strong>startPeriod</strong><br><em>Nullable&#x3C;DateTimeOffset></em> <strong>endPeriod</strong></p> | Find adjustments matching the specified                              |

## Implementations

### Local Stock Management Repository - (SanteDB.Core)

Represents a stock management repository service.

#### Service Registration

```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
    <serviceProviders>
        ...
        <add type="SanteDB.Core.Services.Impl.LocalStockManagementRepositoryService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
        ...
    </serviceProviders>
```

## Example Implementation

```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyStockManagementRepositoryService : SanteDB.Core.Services.IStockManagementRepositoryService { 
    public String ServiceName => "My own IStockManagementRepositoryService service";
    /// <summary>
    /// Performs a stock adjustment for the specified facility and material.
    /// </summary>
    public Act Adjust(ManufacturedMaterial manufacturedMaterial,Place place,Int32 quantity,Concept reason){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Gets the balance for the material.
    /// </summary>
    public Int32 GetBalance(Place place,ManufacturedMaterial manufacturedMaterial){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Get the total amount of consumed objects
    /// </summary>
    public IEnumerable<ActParticipation> GetConsumed(Guid manufacturedMaterialKey,Guid placeKey,Nullable<DateTimeOffset> startPeriod,Nullable<DateTimeOffset> endPeriod){
        throw new System.NotImplementedException();
    }
    /// <summary>
    /// Find adjustments matching the specified
    /// </summary>
    public IEnumerable<Act> FindAdjustments(Guid manufacturedMaterialKey,Guid placeKey,Nullable<DateTimeOffset> startPeriod,Nullable<DateTimeOffset> endPeriod){
        throw new System.NotImplementedException();
    }
}
```

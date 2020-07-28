---
description: IStockManagementRepositoryService (SanteDB.Core.Api)
---

# Stock Management Repository

## Summary

Represents a stock management repository service.

## Operations

| Operation | Response/Return | Input/Parameter | Description |
| :--- | :--- | :--- | :--- |
| Adjust | Act | _ManufacturedMaterial_ **manufacturedMaterial** _Place_ **place** _Int32_ **quantity** _Concept_ **reason** | Performs a stock adjustment for the specified facility and material. |
| GetBalance | Int32 | _Place_ **place** _ManufacturedMaterial_ **manufacturedMaterial** | Gets the balance for the material. |
| GetConsumed | IEnumerable&lt;ActParticipation&gt; | _Guid_ **manufacturedMaterialKey** _Guid_ **placeKey** _Nullable&lt;DateTimeOffset&gt;_ **startPeriod** _Nullable&lt;DateTimeOffset&gt;_ **endPeriod** | Get the total amount of consumed objects |
| FindAdjustments | IEnumerable&lt;Act&gt; | _Guid_ **manufacturedMaterialKey** _Guid_ **placeKey** _Nullable&lt;DateTimeOffset&gt;_ **startPeriod** _Nullable&lt;DateTimeOffset&gt;_ **endPeriod** | Find adjustments matching the specified |

## Implementations

### Local Stock Management Repository - \(SanteDB.Core\)

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


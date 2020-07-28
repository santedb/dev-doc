---
description: IStockManagementRepositoryService (SanteDB.Core.Api)
---

## Summary
Represents a stock management repository service.

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Adjust|SanteDB.Core.Model.Acts.Act|manufacturedMaterial <small style='border:solid 1px #aaa'>SanteDB.Core.Model.Entities.ManufacturedMaterial</small><br/>place <small style='border:solid 1px #aaa'>SanteDB.Core.Model.Entities.Place</small><br/>quantity <small style='border:solid 1px #aaa'>System.Int32</small><br/>reason <small style='border:solid 1px #aaa'>SanteDB.Core.Model.DataTypes.Concept</small>|Performs a stock adjustment for the specified facility and material.|
|GetBalance|System.Int32|place <small style='border:solid 1px #aaa'>SanteDB.Core.Model.Entities.Place</small><br/>manufacturedMaterial <small style='border:solid 1px #aaa'>SanteDB.Core.Model.Entities.ManufacturedMaterial</small>|Gets the balance for the material.|
|GetConsumed|System.Collections.Generic.IEnumerable&lt;SanteDB.Core.Model.Acts.ActParticipation>|manufacturedMaterialKey <small style='border:solid 1px #aaa'>System.Guid</small><br/>placeKey <small style='border:solid 1px #aaa'>System.Guid</small><br/>startPeriod <small style='border:solid 1px #aaa'>System.Nullable<System.DateTimeOffset></small><br/>endPeriod <small style='border:solid 1px #aaa'>System.Nullable<System.DateTimeOffset></small>|Get the total amount of consumed objects|
|FindAdjustments|System.Collections.Generic.IEnumerable&lt;SanteDB.Core.Model.Acts.Act>|manufacturedMaterialKey <small style='border:solid 1px #aaa'>System.Guid</small><br/>placeKey <small style='border:solid 1px #aaa'>System.Guid</small><br/>startPeriod <small style='border:solid 1px #aaa'>System.Nullable<System.DateTimeOffset></small><br/>endPeriod <small style='border:solid 1px #aaa'>System.Nullable<System.DateTimeOffset></small>|Find adjustments matching the specified|

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
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyStockManagementRepositoryService : SanteDB.Core.Services.IStockManagementRepositoryService { 
	public String ServiceName => "My own IStockManagementRepositoryService service";
	/// <summary>
	/// Performs a stock adjustment for the specified facility and material.
	/// </summary>
	public SanteDB.Core.Model.Acts.Act Adjust(SanteDB.Core.Model.Entities.ManufacturedMaterial manufacturedMaterial,SanteDB.Core.Model.Entities.Place place,System.Int32 quantity,SanteDB.Core.Model.DataTypes.Concept reason){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the balance for the material.
	/// </summary>
	public System.Int32 GetBalance(SanteDB.Core.Model.Entities.Place place,SanteDB.Core.Model.Entities.ManufacturedMaterial manufacturedMaterial){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the total amount of consumed objects
	/// </summary>
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Model.Acts.ActParticipation> GetConsumed(System.Guid manufacturedMaterialKey,System.Guid placeKey,System.Nullable<System.DateTimeOffset> startPeriod,System.Nullable<System.DateTimeOffset> endPeriod){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find adjustments matching the specified
	/// </summary>
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Model.Acts.Act> FindAdjustments(System.Guid manufacturedMaterialKey,System.Guid placeKey,System.Nullable<System.DateTimeOffset> startPeriod,System.Nullable<System.DateTimeOffset> endPeriod){
		throw new System.NotImplementedException();
	}
}
```

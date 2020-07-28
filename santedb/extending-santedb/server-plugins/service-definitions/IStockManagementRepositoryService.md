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
|Adjust|Act|manufacturedMaterial <small style='border:solid 1px #aaa'>ManufacturedMaterial</small><br/>place <small style='border:solid 1px #aaa'>Place</small><br/>quantity <small style='border:solid 1px #aaa'>Int32</small><br/>reason <small style='border:solid 1px #aaa'>Concept</small>|Performs a stock adjustment for the specified facility and material.|
|GetBalance|Int32|place <small style='border:solid 1px #aaa'>Place</small><br/>manufacturedMaterial <small style='border:solid 1px #aaa'>ManufacturedMaterial</small>|Gets the balance for the material.|
|GetConsumed|IEnumerable&lt;ActParticipation>|manufacturedMaterialKey <small style='border:solid 1px #aaa'>Guid</small><br/>placeKey <small style='border:solid 1px #aaa'>Guid</small><br/>startPeriod <small style='border:solid 1px #aaa'>Nullable<DateTimeOffset></small><br/>endPeriod <small style='border:solid 1px #aaa'>Nullable<DateTimeOffset></small>|Get the total amount of consumed objects|
|FindAdjustments|IEnumerable&lt;Act>|manufacturedMaterialKey <small style='border:solid 1px #aaa'>Guid</small><br/>placeKey <small style='border:solid 1px #aaa'>Guid</small><br/>startPeriod <small style='border:solid 1px #aaa'>Nullable<DateTimeOffset></small><br/>endPeriod <small style='border:solid 1px #aaa'>Nullable<DateTimeOffset></small>|Find adjustments matching the specified|

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

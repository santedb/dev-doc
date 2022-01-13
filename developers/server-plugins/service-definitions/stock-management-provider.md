`IStockManagementRepositoryService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a stock management repository service.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Adjust|Act|*ManufacturedMaterial* **manufacturedMaterial**<br/>*Place* **place**<br/>*Int32* **quantity**<br/>*Concept* **reason**|Performs a stock adjustment for the specified facility and material.|
|GetBalance|Int32|*Place* **place**<br/>*ManufacturedMaterial* **manufacturedMaterial**|Gets the balance for the material.|
|GetConsumed|IEnumerable&lt;ActParticipation>|*Guid* **manufacturedMaterialKey**<br/>*Guid* **placeKey**<br/>*Nullable&lt;DateTimeOffset>* **startPeriod**<br/>*Nullable&lt;DateTimeOffset>* **endPeriod**|Get the total amount of consumed objects|
|FindAdjustments|IEnumerable&lt;Act>|*Guid* **manufacturedMaterialKey**<br/>*Guid* **placeKey**<br/>*Nullable&lt;DateTimeOffset>* **startPeriod**<br/>*Nullable&lt;DateTimeOffset>* **endPeriod**|Find adjustments matching the specified|

# Implementations


## Local Stock Management Repository - (SanteDB.Server.Core)
Represents a stock management repository service.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalStockManagementRepositoryService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
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

# References

* [IStockManagementRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IStockManagementRepositoryService.htm)
* [LocalStockManagementRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalStockManagementRepositoryService.htm)

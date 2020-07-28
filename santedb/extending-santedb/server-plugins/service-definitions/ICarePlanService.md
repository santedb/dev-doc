---
description: ICarePlanService (SanteDB.Core.Api)
---

## Summary
Represents a class which can create care plans

## Events

|Event|Type|Description|
|-|-|-|

## Properties


## Methods


## Implementations


### Simple Care Planning Service - (SanteDB.Core.Api)
Represents a care plan service that can bundle protocol acts together 
            based on their start/stop times

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Protocol.SimpleCarePlanService, SanteDB.Core.Api, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyCarePlanService : SanteDB.Core.Services.ICarePlanService { 
	public String ServiceName => "My own ICarePlanService service";
	/// <summary>
	/// Gets the list of protocols which can be or should be used to create the care plans
	/// </summary>
	public System.Collections.Generic.List<SanteDB.Core.Protocol.IClinicalProtocol> Protocols {
		get;
	}
	/// <summary>
	/// Create a care plam
	/// </summary>
	public SanteDB.Core.Model.Acts.CarePlan CreateCarePlan(SanteDB.Core.Model.Roles.Patient p){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a care plam
	/// </summary>
	public SanteDB.Core.Model.Acts.CarePlan CreateCarePlan(SanteDB.Core.Model.Roles.Patient p,System.Boolean asEncounters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a care plam
	/// </summary>
	public SanteDB.Core.Model.Acts.CarePlan CreateCarePlan(SanteDB.Core.Model.Roles.Patient p,System.Boolean asEncounters,System.Collections.Generic.IDictionary<System.String,System.Object> parameters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a care plam
	/// </summary>
	public SanteDB.Core.Model.Acts.CarePlan CreateCarePlan(SanteDB.Core.Model.Roles.Patient p,System.Boolean asEncounters,System.Collections.Generic.IDictionary<System.String,System.Object> parameters,System.Guid[] protocols){
		throw new System.NotImplementedException();
	}
}
```

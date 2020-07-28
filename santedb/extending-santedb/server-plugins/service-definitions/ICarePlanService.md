---
description: ICarePlanService (SanteDB.Core.Api)
---

## Summary
Represents a class which can create care plans

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Protocols|List&lt;IClinicalProtocol>|R|Gets the list of protocols which can be or should be used to create the care plans|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|CreateCarePlan|CarePlan|p <small style='border:solid 1px #aaa'>Patient</small>|Create a care plam|
|CreateCarePlan|CarePlan|p <small style='border:solid 1px #aaa'>Patient</small><br/>asEncounters <small style='border:solid 1px #aaa'>Boolean</small>|Create a care plam|
|CreateCarePlan|CarePlan|p <small style='border:solid 1px #aaa'>Patient</small><br/>asEncounters <small style='border:solid 1px #aaa'>Boolean</small><br/>parameters <small style='border:solid 1px #aaa'>IDictionary<String,Object></small>|Create a care plam|
|CreateCarePlan|CarePlan|p <small style='border:solid 1px #aaa'>Patient</small><br/>asEncounters <small style='border:solid 1px #aaa'>Boolean</small><br/>parameters <small style='border:solid 1px #aaa'>IDictionary<String,Object></small><br/>protocols <small style='border:solid 1px #aaa'>Guid[]</small>|Create a care plam|

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
	public List<IClinicalProtocol> Protocols {
		get;
	}
	/// <summary>
	/// Create a care plam
	/// </summary>
	public CarePlan CreateCarePlan(Patient p){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a care plam
	/// </summary>
	public CarePlan CreateCarePlan(Patient p,Boolean asEncounters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a care plam
	/// </summary>
	public CarePlan CreateCarePlan(Patient p,Boolean asEncounters,IDictionary<String,Object> parameters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a care plam
	/// </summary>
	public CarePlan CreateCarePlan(Patient p,Boolean asEncounters,IDictionary<String,Object> parameters,Guid[] protocols){
		throw new System.NotImplementedException();
	}
}
```

`ICarePlanService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Service contract for service implementations which generate [CarePlan](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_CarePlan.htm) instances

## Description
The care plan generator is responsible for using the [IClinicalProtocolRepositoryService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IClinicalProtocolRepositoryService.htm) (which 
            stores and manages [IClinicalProtocol](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Protocol_IClinicalProtocol.htm) instances) to generate instances of patient [CarePlan](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_CarePlan.htm)
            objects which can then be conveyed to the caller and/or stored in the primary CDR.

# Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Protocols|IList&lt;IClinicalProtocol>|R|Gets the list of protocols which can be or should be used to create the care plans|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|CreateCarePlan|CarePlan|*Patient* **patient**|Create a new care plan (using all available protocols for which the patient is eligible)|
|CreateCarePlan|CarePlan|*Patient* **patient**<br/>*Boolean* **groupAsEncounters**|Create a new care plan (using all available protocols for which the patient is eligible)|
|CreateCarePlan|CarePlan|*Patient* **patient**<br/>*Boolean* **groupAsEncounters**<br/>*IDictionary&lt;String,Object>* **parameters**|Create a new care plan (using all available protocols for which the patient is eligible)|
|CreateCarePlan|CarePlan|*Patient* **patient**<br/>*Boolean* **groupAsEncounters**<br/>*IDictionary&lt;String,Object>* **parameters**<br/>*Guid[]* **protocols**|Create a new care plan (using all available protocols for which the patient is eligible)|

# Implementations


## Default Care Planning Service - (SanteDB.Core.Api)
Represents a care plan service that can bundle protocol acts together based on their start/stop times
### Description
This implementation of the care plan service is capable of calling [IClinicalProtocol](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Protocol_IClinicalProtocol.htm) instances
            registered from the clinical protocol manager to construct [Act](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_Act.htm) instances representing the proposed
            actions to take for the patient. The care planner is also capable of simple interval hull functions to group 
            these acts together into [PatientEncounter](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_PatientEncounter.htm) instances based on safe time for grouping.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Protocol.SimpleCarePlanService, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyCarePlanService : SanteDB.Core.Services.ICarePlanService { 
	public String ServiceName => "My own ICarePlanService service";
	/// <summary>
	/// Gets the list of protocols which can be or should be used to create the care plans
	/// </summary>
	public IList<IClinicalProtocol> Protocols {
		get;
	}
	/// <summary>
	/// Create a new care plan (using all available protocols for which the patient is eligible)
	/// </summary>
	public CarePlan CreateCarePlan(Patient patient){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a new care plan (using all available protocols for which the patient is eligible)
	/// </summary>
	public CarePlan CreateCarePlan(Patient patient,Boolean groupAsEncounters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a new care plan (using all available protocols for which the patient is eligible)
	/// </summary>
	public CarePlan CreateCarePlan(Patient patient,Boolean groupAsEncounters,IDictionary<String,Object> parameters){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a new care plan (using all available protocols for which the patient is eligible)
	/// </summary>
	public CarePlan CreateCarePlan(Patient patient,Boolean groupAsEncounters,IDictionary<String,Object> parameters,Guid[] protocols){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ICarePlanService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ICarePlanService.htm)
* [SimpleCarePlanService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Protocol_SimpleCarePlanService.htm)

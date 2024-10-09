`IDecisionSupportService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Service contract for service implementations which generate [CarePlan](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_CarePlan.htm) instances

## Description
The care plan generator is responsible for using the [!:IClinicalProtocolRepositoryService](#!:IClinicalProtocolRepositoryService) (which 
            stores and manages [ICdssProtocol](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Cdss_ICdssProtocol.htm) instances) to generate instances of patient [CarePlan](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_CarePlan.htm)
            objects which can then be conveyed to the caller and/or stored in the primary CDR.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|CreateCarePlan|CarePlan|*Patient* **patient**|Create a new care plan (using all available protocols for which the patient is eligible)|
|CreateCarePlan|CarePlan|*Patient* **patient**<br/>*Boolean* **groupAsEncounters**|Create a new care plan (using all available protocols for which the patient is eligible)|
|CreateCarePlan|CarePlan|*Patient* **patient**<br/>*Boolean* **groupAsEncounters**<br/>*IDictionary&lt;String,Object>* **parameters**<br/>*ICdssLibrary[]* **librariesToUse**|Create a new care plan (using all available protocols for which the patient is eligible)|
|Analyze|IEnumerable&lt;DetectedIssue>|*Act* **collectedData**<br/>*ICdssLibrary[]* **librariesToApply**|Instructs the implementation to analyze the data for  according to the protocols specified in|
|AnalyzeGlobal|IEnumerable&lt;DetectedIssue>|*Act* **collectedData**|Instructs the implementation to analyze the data provided in  using every registered clinical protocol in the             SanteDB instance.|

# Implementations


## SimpleCarePlanService - (SanteDB.Core.Api)
Type redirect

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Cdss.SimpleCarePlanService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Default Care Planning Service - (SanteDB.Core.Api)
Represents a care plan service that can bundle protocol acts together based on their start/stop times
### Description
This implementation of the care plan service is capable of calling [ICdssProtocol](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Cdss_ICdssProtocol.htm) instances
            registered from the clinical protocol manager to construct [Act](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_Act.htm) instances representing the proposed
            actions to take for the patient. The care planner is also capable of simple interval hull functions to group 
            these acts together into [PatientEncounter](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_PatientEncounter.htm) instances based on safe time for grouping.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Cdss.SimpleDecisionSupportService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyDecisionSupportService : SanteDB.Core.Services.IDecisionSupportService { 
	public String ServiceName => "My own IDecisionSupportService service";
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
	public CarePlan CreateCarePlan(Patient patient,Boolean groupAsEncounters,IDictionary<String,Object> parameters,ICdssLibrary[] librariesToUse){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Instructs the implementation to analyze the data for  according to the protocols specified in
	/// </summary>
	public IEnumerable<DetectedIssue> Analyze(Act collectedData,ICdssLibrary[] librariesToApply){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Instructs the implementation to analyze the data provided in  using every registered clinical protocol in the             SanteDB instance.
	/// </summary>
	public IEnumerable<DetectedIssue> AnalyzeGlobal(Act collectedData){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDecisionSupportService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDecisionSupportService.htm)
* [SimpleCarePlanService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Cdss_SimpleCarePlanService.htm)
* [SimpleDecisionSupportService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Cdss_SimpleDecisionSupportService.htm)

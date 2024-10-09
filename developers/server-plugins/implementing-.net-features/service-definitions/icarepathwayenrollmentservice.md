`ICarePathwayEnrollmentService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Service which manages the enrolment of patients into care pathways

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetEligibleCarePaths|IEnumerable&lt;CarePathwayDefinition>|*Patient* **patient**|Gets the carepaths that the  meets eligibility criteria for|
|GetEnrolledCarePaths|IEnumerable&lt;CarePathwayDefinition>|*Patient* **patient**|Get all the care pathways in which the patient is enrolled (i.e. has an active care plan)|
|Enroll|CarePlan|*Patient* **patient**<br/>*CarePathwayDefinition* **carePathway**|Enrol the patient in the specified|
|Enroll|CarePlan|*Patient* **patient**<br/>*Guid* **carePathwayKey**|Enrol the patient in the specified|
|UnEnroll|CarePlan|*Patient* **patient**<br/>*CarePathwayDefinition* **carePathway**|Un-enrols the patient from the|
|UnEnroll|CarePlan|*Patient* **patient**<br/>*Guid* **carePathwayKey**|Un-enrols the patient from the|
|TryGetEnrollment|Boolean|*Patient* **patient**<br/>*CarePathwayDefinition* **carePathway**<br/>*CarePlan&* **carePlan**|Determines if  is enrolled in|
|TryGetEnrollment|Boolean|*Patient* **patient**<br/>*Guid* **carePathwayKey**<br/>*CarePlan&* **carePlan**|Determines if  is enrolled in|

# Implementations


## DefaultCarepathEnrollmentService - (SanteDB.Core.Api)
Default carepath enrolment service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.DefaultCarepathEnrollmentService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyCarePathwayEnrollmentService : SanteDB.Core.Services.ICarePathwayEnrollmentService { 
	public String ServiceName => "My own ICarePathwayEnrollmentService service";
	/// <summary>
	/// Gets the carepaths that the  meets eligibility criteria for
	/// </summary>
	public IEnumerable<CarePathwayDefinition> GetEligibleCarePaths(Patient patient){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all the care pathways in which the patient is enrolled (i.e. has an active care plan)
	/// </summary>
	public IEnumerable<CarePathwayDefinition> GetEnrolledCarePaths(Patient patient){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Enrol the patient in the specified
	/// </summary>
	public CarePlan Enroll(Patient patient,CarePathwayDefinition carePathway){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Enrol the patient in the specified
	/// </summary>
	public CarePlan Enroll(Patient patient,Guid carePathwayKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Un-enrols the patient from the
	/// </summary>
	public CarePlan UnEnroll(Patient patient,CarePathwayDefinition carePathway){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Un-enrols the patient from the
	/// </summary>
	public CarePlan UnEnroll(Patient patient,Guid carePathwayKey){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Determines if  is enrolled in
	/// </summary>
	public Boolean TryGetEnrollment(Patient patient,CarePathwayDefinition carePathway,CarePlan& carePlan){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Determines if  is enrolled in
	/// </summary>
	public Boolean TryGetEnrollment(Patient patient,Guid carePathwayKey,CarePlan& carePlan){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ICarePathwayEnrollmentService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ICarePathwayEnrollmentService.htm)
* [DefaultCarepathEnrollmentService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_DefaultCarepathEnrollmentService.htm)

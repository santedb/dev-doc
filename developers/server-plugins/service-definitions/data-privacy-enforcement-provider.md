`IPrivacyEnforcementService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Contract for services which enforce privacy directives

## Description
Implementers of this service contract are expected to provide support for the 
            [SanteDB Privacy Enforcement](https://help.santesuite.org/santedb/privacy-architecture) architecture. The responsibilities for 
            implementers are:

* Enforce the data privacy directives attached to [Entity](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Entities_Entity.htm) or [Act](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_Act.htm) instances prior to disclosure of the record (for example: redact, mask, or hide)
* Ensure that data privacy directives are adhered to prior to updating data in the CDR
* Ensure that fields which are sensitive or forbidden are not being used in queries


This service is used by the [IRepositoryService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRepositoryService.htm) layer. ValidateWrite is used prior to executing a
            write operation should ensure that the data being provided/written does not violate local privacy laws (i.e. if Race is forbidden, and the 
            request contains Race the request should be aborted or scrubbed)

Additionally, the ValidateQuery method is invoked prior to querying to ensure that the query parameters don't
            violate local privacy laws (i.e. don't permit query on MaritalStatus) and that patient privacy policies would not be violated by the query.
            For example, if the jurisdiction has a policy which protects or hides ```HIV_PROGRAM``` identifiers, and a principal which lacks that policy
            attempts a query such as ```identifier[HIV_PROGRAM].value=!null```, then patient privacy could be compromised just by the nature of a 
            a result being returned (even it if the HIV_PROGRAM identifier is scrubbed). The ValidateQuery method should protect in these
            cases (note: the default implementation does not protect against this, however the capability is present for third party implementers of this service
            to produce such behavior)

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Apply|TData|*TData* **data**<br/>*IPrincipal* **principal**|Applies the privacy policies attached to the provided data such that a disclosure to the provided principal would            not compromise patient privacy.|
|Apply|IEnumerable&lt;TData>|*IEnumerable&lt;TData>* **data**<br/>*IPrincipal* **principal**|Applies the privacy policies attached to the provided data such that a disclosure to the provided principal would            not compromise patient privacy.|
|ValidateWrite|Boolean|*TData* **data**<br/>*IPrincipal* **principal**|Determine if the record provided contains data that the user             shouldn't be sending.|
|ValidateQuery|Boolean|*Expression&lt;Func&lt;TModel,Boolean>>* **query**<br/>*IPrincipal* **principal**|Validate that a query can be performed by user  and does not contain forbidden or compromising fields|

# Implementations


## Data Privacy Filtering - (SanteDB.Core.Api)
Local policy enforcement point service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.Privacy.DataPolicyFilterService, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## ExemptablePolicyFilterService - (SanteDB.Server.Core)
Local policy enforcement point service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Security.Privacy.ExemptablePolicyFilterService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security;
/// Other usings here
public class MyPrivacyEnforcementService : SanteDB.Core.Security.IPrivacyEnforcementService { 
	public String ServiceName => "My own IPrivacyEnforcementService service";
	/// <summary>
	/// Applies the privacy policies attached to the provided data such that a disclosure to the provided principal would            not compromise patient privacy.
	/// </summary>
	public TData Apply<TData>(TData data,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Applies the privacy policies attached to the provided data such that a disclosure to the provided principal would            not compromise patient privacy.
	/// </summary>
	public IEnumerable<TData> Apply<TData>(IEnumerable<TData> data,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Determine if the record provided contains data that the user             shouldn't be sending.
	/// </summary>
	public Boolean ValidateWrite<TData>(TData data,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Validate that a query can be performed by user  and does not contain forbidden or compromising fields
	/// </summary>
	public Boolean ValidateQuery<TModel>(Expression<Func<TModel,Boolean>> query,IPrincipal principal){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IPrivacyEnforcementService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_IPrivacyEnforcementService.htm)
* [DataPolicyFilterService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Privacy_DataPolicyFilterService.htm)
* [ExemptablePolicyFilterService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Security_Privacy_ExemptablePolicyFilterService.htm)

---
description: Data Privacy Provider (IPrivacyEnforcementService in SanteDB.Core.Api)
---

# Summary
Privacy enforcement service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Apply|TData|*TData* **data**<br/>*IPrincipal* **principal**|Apply all privacy policies|
|Apply|IEnumerable&lt;TData>|*IEnumerable&lt;TData>* **data**<br/>*IPrincipal* **principal**|Apply all privacy policies|
|ValidateWrite|Boolean|*TData* **data**<br/>*IPrincipal* **principal**|Determine if the record provided contains data that the             shouldn't be sending such as masked identifiers or the record itself (due to access permission)|
|ValidateQuery|Boolean|*Expression&lt;Func&lt;TModel,Boolean>>* **query**<br/>*IPrincipal* **principal**|Validate that a query can be performed by|

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
	/// Apply all privacy policies
	/// </summary>
	public TData Apply<TData>(TData data,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Apply all privacy policies
	/// </summary>
	public IEnumerable<TData> Apply<TData>(IEnumerable<TData> data,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Determine if the record provided contains data that the             shouldn't be sending such as masked identifiers or the record itself (due to access permission)
	/// </summary>
	public Boolean ValidateWrite<TData>(TData data,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Validate that a query can be performed by
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

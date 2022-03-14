`IPolicyInformationService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a contract for a policy information service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetPolicies|IEnumerable&lt;IPolicyInstance>|*Object* **securable**|Get all active policies for the specified securable type|
|GetPolicies|IEnumerable&lt;IPolicy>|*none*|Get all active policies for the specified securable type|
|GetPolicy|IPolicy|*String* **policyOid**|Get a specific policy|
|AddPolicies|void|*Object* **securable**<br/>*PolicyGrantType* **rule**<br/>*IPrincipal* **principal**<br/>*String[]* **policyOids**|Adds the specified policies to the specified securable object|
|GetPolicyInstance|IPolicyInstance|*Object* **securable**<br/>*String* **policyOid**|Gets the policy instance for the specified object|
|RemovePolicies|void|*Object* **securable**<br/>*IPrincipal* **principal**<br/>*String[]* **oid**|Removes the specified policies from the user account|

# Implementations


## ADO.NET Policy Information Service - (SanteDB.Persistence.Data.ADO)
Represents a PIP fed from SQL Server tables

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoPolicyInformationService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyPolicyInformationService : SanteDB.Core.Security.Services.IPolicyInformationService { 
	public String ServiceName => "My own IPolicyInformationService service";
	/// <summary>
	/// Get all active policies for the specified securable type
	/// </summary>
	public IEnumerable<IPolicyInstance> GetPolicies(Object securable){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all active policies for the specified securable type
	/// </summary>
	public IEnumerable<IPolicy> GetPolicies(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a specific policy
	/// </summary>
	public IPolicy GetPolicy(String policyOid){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Adds the specified policies to the specified securable object
	/// </summary>
	public void AddPolicies(Object securable,PolicyGrantType rule,IPrincipal principal,String[] policyOids){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the policy instance for the specified object
	/// </summary>
	public IPolicyInstance GetPolicyInstance(Object securable,String policyOid){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes the specified policies from the user account
	/// </summary>
	public void RemovePolicies(Object securable,IPrincipal principal,String[] oid){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IPolicyInformationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IPolicyInformationService.htm)
* [AdoPolicyInformationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoPolicyInformationService.htm)

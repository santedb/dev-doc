`IPolicyDecisionService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a policy decision service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetEffectivePolicySet|IEnumerable&lt;IPolicyInstance>|*IPrincipal* **securable**|Get all active policies for the specified securable type|
|GetPolicyDecision|PolicyDecision|*IPrincipal* **principal**<br/>*Object* **securable**|Make a simple policy decision for a specific securable|
|GetPolicyOutcome|PolicyGrantType|*IPrincipal* **principal**<br/>*String* **policyId**|Get a policy decision outcome (i.e. make a policy decision)|
|ClearCache|void|*IPrincipal* **principal**|Clear the policy cache for the specified principal|
|ClearCache|void|*String* **principalName**|Clear the policy cache for the specified principal|

# Implementations


## Default PDP Service - (SanteDB.Core.Api)
Local policy decision service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.DefaultPolicyDecisionService, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyPolicyDecisionService : SanteDB.Core.Security.Services.IPolicyDecisionService { 
	public String ServiceName => "My own IPolicyDecisionService service";
	/// <summary>
	/// Get all active policies for the specified securable type
	/// </summary>
	public IEnumerable<IPolicyInstance> GetEffectivePolicySet(IPrincipal securable){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Make a simple policy decision for a specific securable
	/// </summary>
	public PolicyDecision GetPolicyDecision(IPrincipal principal,Object securable){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a policy decision outcome (i.e. make a policy decision)
	/// </summary>
	public PolicyGrantType GetPolicyOutcome(IPrincipal principal,String policyId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Clear the policy cache for the specified principal
	/// </summary>
	public void ClearCache(IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Clear the policy cache for the specified principal
	/// </summary>
	public void ClearCache(String principalName){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IPolicyDecisionService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IPolicyDecisionService.htm)
* [DefaultPolicyDecisionService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_DefaultPolicyDecisionService.htm)

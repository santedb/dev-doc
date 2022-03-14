`IPolicyEnforcementService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a PEP that receives demands

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Demand|void|*String* **policyId**|Demand access to the policy|
|Demand|void|*String* **policyId**<br/>*IPrincipal* **principal**|Demand access to the policy|
|SoftDemand|Boolean|*String* **policyId**<br/>*IPrincipal* **principal**|Demand the specified policy and return the result|

# Implementations


## DefaultPolicyEnforcementService - (SanteDB.Core.Api)
Policy enforcement service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.DefaultPolicyEnforcementService, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## DcApplicationContext - (SanteDB.DisconnectedClient.UI)
Test application context

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.DisconnectedClient.UI.DcApplicationContext, SanteDB.DisconnectedClient.UI, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## DefaultPolicyEnforcementService - (SanteDB.Server.Core)
Policy enforcement service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.DefaultPolicyEnforcementService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyPolicyEnforcementService : SanteDB.Core.Security.Services.IPolicyEnforcementService { 
	public String ServiceName => "My own IPolicyEnforcementService service";
	/// <summary>
	/// Demand access to the policy
	/// </summary>
	public void Demand(String policyId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Demand access to the policy
	/// </summary>
	public void Demand(String policyId,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Demand the specified policy and return the result
	/// </summary>
	public Boolean SoftDemand(String policyId,IPrincipal principal){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IPolicyEnforcementService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IPolicyEnforcementService.htm)
* [DefaultPolicyEnforcementService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_DefaultPolicyEnforcementService.htm)
* [DcApplicationContext C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_DisconnectedClient_UI_DcApplicationContext.htm)
* [DefaultPolicyEnforcementService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_DefaultPolicyEnforcementService.htm)

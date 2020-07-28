---
description: IPolicyDecisionService (SanteDB.Core.Api)
---

## Summary
Represents a policy decision service

## Implementations


### Default PDP Service - (SanteDB.Core)
Local policy decision service

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.DefaultPolicyDecisionService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyPolicyDecisionService : SanteDB.Core.Security.Services.IPolicyDecisionService { 
	public String ServiceName => "My own IPolicyDecisionService service";
	/// <summary>
	/// Make a simple policy decision for a specific securable
	/// </summary>
	public SanteDB.Core.Security.PolicyDecision GetPolicyDecision(System.Security.Principal.IPrincipal principal,System.Object securable){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a policy decision outcome (i.e. make a policy decision)
	/// </summary>
	public SanteDB.Core.Model.Security.PolicyGrantType GetPolicyOutcome(System.Security.Principal.IPrincipal principal,System.String policyId){
		throw new System.NotImplementedException();
	}
}
```

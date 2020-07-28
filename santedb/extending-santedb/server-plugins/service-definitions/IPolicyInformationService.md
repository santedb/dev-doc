---
description: IPolicyInformationService (SanteDB.Core.Api)
---

## Summary
Represents a contract for a policy information service

## Events

|Event|Type|Description|
|-|-|-|

## Properties


## Methods


## Implementations


### ADO.NET Policy Information Service - (SanteDB.Persistence.Data.ADO)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoPolicyInformationService, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyPolicyInformationService : SanteDB.Core.Security.Services.IPolicyInformationService { 
	public String ServiceName => "My own IPolicyInformationService service";
	/// <summary>
	/// Get active policies for the specified securable type
	/// </summary>
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Security.IPolicyInstance> GetActivePolicies(System.Object securable){
		throw new System.NotImplementedException();
	}
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Security.IPolicy> GetPolicies(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get a specific policy
	/// </summary>
	public SanteDB.Core.Security.IPolicy GetPolicy(System.String policyOid){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Adds the specified policies to the specified securable object
	/// </summary>
	public void AddPolicies(System.Object securable,SanteDB.Core.Model.Security.PolicyGrantType rule,System.Security.Principal.IPrincipal principal,System.String[] policyOids){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the policy instance for the specified object
	/// </summary>
	public SanteDB.Core.Security.IPolicyInstance GetPolicyInstance(System.Object securable,System.String policyOid){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes the specified policies from the user account
	/// </summary>
	public void RemovePolicies(System.Object securable,System.Security.Principal.IPrincipal principal,System.String[] oid){
		throw new System.NotImplementedException();
	}
}
```

---
description: IPolicyInformationService (SanteDB.Core.Api)
---

## Summary
Represents a contract for a policy information service

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetActivePolicies|IEnumerable&lt;IPolicyInstance>|*Object* **securable**|Get active policies for the specified securable type|
|GetPolicies|IEnumerable&lt;IPolicy>||TODO|
|GetPolicy|IPolicy|*String* **policyOid**|Get a specific policy|
|AddPolicies|void|*Object* **securable**<br/>*PolicyGrantType* **rule**<br/>*IPrincipal* **principal**<br/>*String[]* **policyOids**|Adds the specified policies to the specified securable object|
|GetPolicyInstance|IPolicyInstance|*Object* **securable**<br/>*String* **policyOid**|Gets the policy instance for the specified object|
|RemovePolicies|void|*Object* **securable**<br/>*IPrincipal* **principal**<br/>*String[]* **oid**|Removes the specified policies from the user account|

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
	public IEnumerable<IPolicyInstance> GetActivePolicies(Object securable){
		throw new System.NotImplementedException();
	}
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

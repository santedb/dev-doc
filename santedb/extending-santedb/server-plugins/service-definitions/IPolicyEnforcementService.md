---
description: IPolicyEnforcementService (SanteDB.Core.Api)
---

## Summary
Represents a PEP that receives demands

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Demand|void|*String* **policyId**|Demand access to the policy|
|Demand|void|*String* **policyId**<br/>*IPrincipal* **principal**|Demand access to the policy|

## Implementations


### ApplicationContext - (SanteDB.Core)
Provides a context for components.

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.ApplicationContext, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

### TestApplicationContext - (SanteDB.Core.TestFramework)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.TestFramework.TestApplicationContext, SanteDB.Core.TestFramework, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
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
}
```

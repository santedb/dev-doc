---
description: ISecurityChallengeService (SanteDB.Core.Api)
---

## Summary
Represents an interface that allows for the retrieval of pre-configured security challenges

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Get|IEnumerable&lt;SecurityChallenge>|*String* **userName**<br/>*IPrincipal* **principal**|Gets the challenges current registered for the user (not the answers)|
|Set|void|*String* **userName**<br/>*Guid* **challengeKey**<br/>*String* **response**<br/>*IPrincipal* **principal**|Add a challenge to the current registered user|
|Remove|void|*String* **userName**<br/>*Guid* **challengeKey**<br/>*IPrincipal* **principal**|Removes or clears the specified challenge|

## Implementations


### AdoSecurityChallengeProvider - (SanteDB.Persistence.Data.ADO)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoSecurityChallengeProvider, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Security;
/// Other usings here
public class MySecurityChallengeService : SanteDB.Core.Security.ISecurityChallengeService { 
	public String ServiceName => "My own ISecurityChallengeService service";
	/// <summary>
	/// Gets the challenges current registered for the user (not the answers)
	/// </summary>
	public IEnumerable<SecurityChallenge> Get(String userName,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Add a challenge to the current registered user
	/// </summary>
	public void Set(String userName,Guid challengeKey,String response,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes or clears the specified challenge
	/// </summary>
	public void Remove(String userName,Guid challengeKey,IPrincipal principal){
		throw new System.NotImplementedException();
	}
}
```

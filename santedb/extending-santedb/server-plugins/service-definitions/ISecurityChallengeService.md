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
|Get|System.Collections.Generic.IEnumerable&lt;SanteDB.Core.Model.Security.SecurityChallenge>|userName <small style='border:solid 1px #aaa'>System.String</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Gets the challenges current registered for the user (not the answers)|
|Set|void|userName <small style='border:solid 1px #aaa'>System.String</small><br/>challengeKey <small style='border:solid 1px #aaa'>System.Guid</small><br/>response <small style='border:solid 1px #aaa'>System.String</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Add a challenge to the current registered user|
|Remove|void|userName <small style='border:solid 1px #aaa'>System.String</small><br/>challengeKey <small style='border:solid 1px #aaa'>System.Guid</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Removes or clears the specified challenge|

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
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Model.Security.SecurityChallenge> Get(System.String userName,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Add a challenge to the current registered user
	/// </summary>
	public void Set(System.String userName,System.Guid challengeKey,System.String response,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes or clears the specified challenge
	/// </summary>
	public void Remove(System.String userName,System.Guid challengeKey,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
}
```

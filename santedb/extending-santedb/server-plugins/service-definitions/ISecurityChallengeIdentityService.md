---
description: ISecurityChallengeIdentityService (SanteDB.Core.Api)
---

## Summary
Represents a security challenge service which can provide identity

## Events

|Event|Type|Description|
|-|-|-|
|Authenticating|System.EventHandler&lt;SanteDB.Core.Security.Services.AuthenticatingEventArgs>|Fired prior to an authentication event|
|Authenticated|System.EventHandler&lt;SanteDB.Core.Security.Services.AuthenticatedEventArgs>|Fired after an authentication decision being made|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Authenticate|System.Security.Principal.IPrincipal|userName <small style='border:solid 1px #aaa'>System.String</small><br/>challengeKey <small style='border:solid 1px #aaa'>System.Guid</small><br/>response <small style='border:solid 1px #aaa'>System.String</small><br/>tfaSecret <small style='border:solid 1px #aaa'>System.String</small>|Authenticates the specified user with a challenge key and response|

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
public class MySecurityChallengeIdentityService : SanteDB.Core.Security.ISecurityChallengeIdentityService { 
	public String ServiceName => "My own ISecurityChallengeIdentityService service";
	/// <summary>
	/// Fired prior to an authentication event
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Security.Services.AuthenticatingEventArgs> Authenticating;
	/// <summary>
	/// Fired after an authentication decision being made
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Security.Services.AuthenticatedEventArgs> Authenticated;
	/// <summary>
	/// Authenticates the specified user with a challenge key and response
	/// </summary>
	public System.Security.Principal.IPrincipal Authenticate(System.String userName,System.Guid challengeKey,System.String response,System.String tfaSecret){
		throw new System.NotImplementedException();
	}
}
```

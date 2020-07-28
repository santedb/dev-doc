---
description: IApplicationIdentityProviderService (SanteDB.Core.Api)
---

## Summary
Represents a service which retrieves IPrincipal objects for applications.

## Events

|Event|Type|Description|
|-|-|-|
|Authenticated|System.EventHandler&lt;SanteDB.Core.Security.Services.AuthenticatedEventArgs>|Fired after an authentication request has been made.|
|Authenticating|System.EventHandler&lt;SanteDB.Core.Security.Services.AuthenticatingEventArgs>|Fired prior to an authentication request being made.|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Authenticate|System.Security.Principal.IPrincipal|applicationId <small style='border:solid 1px #aaa'>System.String</small><br/>applicationSecret <small style='border:solid 1px #aaa'>System.String</small>|Authenticate the application identity.|
|GetIdentity|System.Security.Principal.IIdentity|name <small style='border:solid 1px #aaa'>System.String</small>|Gets the specified identity for an application.|
|SetLockout|void|name <small style='border:solid 1px #aaa'>System.String</small><br/>lockoutState <small style='border:solid 1px #aaa'>System.Boolean</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Set the lockout status|
|ChangeSecret|void|name <small style='border:solid 1px #aaa'>System.String</small><br/>secret <small style='border:solid 1px #aaa'>System.String</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Change the specified application identity's secret|

## Implementations


### ADO.NET Application Identity Provider - (SanteDB.Persistence.Data.ADO)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoApplicationIdentityProvider, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyApplicationIdentityProviderService : SanteDB.Core.Security.Services.IApplicationIdentityProviderService { 
	public String ServiceName => "My own IApplicationIdentityProviderService service";
	/// <summary>
	/// Fired after an authentication request has been made.
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Security.Services.AuthenticatedEventArgs> Authenticated;
	/// <summary>
	/// Fired prior to an authentication request being made.
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Security.Services.AuthenticatingEventArgs> Authenticating;
	/// <summary>
	/// Authenticate the application identity.
	/// </summary>
	public System.Security.Principal.IPrincipal Authenticate(System.String applicationId,System.String applicationSecret){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified identity for an application.
	/// </summary>
	public System.Security.Principal.IIdentity GetIdentity(System.String name){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Set the lockout status
	/// </summary>
	public void SetLockout(System.String name,System.Boolean lockoutState,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Change the specified application identity's secret
	/// </summary>
	public void ChangeSecret(System.String name,System.String secret,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
}
```

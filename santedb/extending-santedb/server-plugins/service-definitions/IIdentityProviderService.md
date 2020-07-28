---
description: IIdentityProviderService (SanteDB.Core.Api)
---

## Summary
Identity provider service

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
|GetIdentity|System.Security.Principal.IIdentity|userName <small style='border:solid 1px #aaa'>System.String</small>|Retrieves an identity from the object|
|GetIdentity|System.Security.Principal.IIdentity|sid <small style='border:solid 1px #aaa'>System.Guid</small>|Retrieves an identity from the object|
|CreateIdentity|System.Security.Principal.IIdentity|userName <small style='border:solid 1px #aaa'>System.String</small><br/>password <small style='border:solid 1px #aaa'>System.String</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Create a basic identity in the provider|
|Authenticate|System.Security.Principal.IPrincipal|userName <small style='border:solid 1px #aaa'>System.String</small><br/>password <small style='border:solid 1px #aaa'>System.String</small>|Authenticate the user creating an identity|
|Authenticate|System.Security.Principal.IPrincipal|userName <small style='border:solid 1px #aaa'>System.String</small><br/>password <small style='border:solid 1px #aaa'>System.String</small><br/>tfaSecret <small style='border:solid 1px #aaa'>System.String</small>|Authenticate the user creating an identity|
|ReAuthenticate|System.Security.Principal.IPrincipal|principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Perform a re-authentication of the principal|
|ChangePassword|void|userName <small style='border:solid 1px #aaa'>System.String</small><br/>newPassword <small style='border:solid 1px #aaa'>System.String</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Change user password|
|GenerateTfaSecret|System.String|userName <small style='border:solid 1px #aaa'>System.String</small>|Set the user's two factor authentication secret|
|DeleteIdentity|void|userName <small style='border:solid 1px #aaa'>System.String</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Delete an identity|
|SetLockout|void|userName <small style='border:solid 1px #aaa'>System.String</small><br/>lockout <small style='border:solid 1px #aaa'>System.Boolean</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Set lockout|
|AddClaim|void|userName <small style='border:solid 1px #aaa'>System.String</small><br/>claim <small style='border:solid 1px #aaa'>SanteDB.Core.Security.Claims.IClaim</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small><br/>expiriy <small style='border:solid 1px #aaa'>System.Nullable<System.TimeSpan></small>|Adds a claim to the specified user account|
|RemoveClaim|void|userName <small style='border:solid 1px #aaa'>System.String</small><br/>claimType <small style='border:solid 1px #aaa'>System.String</small><br/>principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small>|Removes a claim from the specified user account|

## Implementations


### ADO.NET Identity Provider - (SanteDB.Persistence.Data.ADO)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoIdentityProvider, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyIdentityProviderService : SanteDB.Core.Security.Services.IIdentityProviderService { 
	public String ServiceName => "My own IIdentityProviderService service";
	/// <summary>
	/// Fired prior to an authentication event
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Security.Services.AuthenticatingEventArgs> Authenticating;
	/// <summary>
	/// Fired after an authentication decision being made
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Security.Services.AuthenticatedEventArgs> Authenticated;
	/// <summary>
	/// Retrieves an identity from the object
	/// </summary>
	public System.Security.Principal.IIdentity GetIdentity(System.String userName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Retrieves an identity from the object
	/// </summary>
	public System.Security.Principal.IIdentity GetIdentity(System.Guid sid){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a basic identity in the provider
	/// </summary>
	public System.Security.Principal.IIdentity CreateIdentity(System.String userName,System.String password,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Authenticate the user creating an identity
	/// </summary>
	public System.Security.Principal.IPrincipal Authenticate(System.String userName,System.String password){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Authenticate the user creating an identity
	/// </summary>
	public System.Security.Principal.IPrincipal Authenticate(System.String userName,System.String password,System.String tfaSecret){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Perform a re-authentication of the principal
	/// </summary>
	public System.Security.Principal.IPrincipal ReAuthenticate(System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Change user password
	/// </summary>
	public void ChangePassword(System.String userName,System.String newPassword,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Set the user's two factor authentication secret
	/// </summary>
	public System.String GenerateTfaSecret(System.String userName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Delete an identity
	/// </summary>
	public void DeleteIdentity(System.String userName,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Set lockout
	/// </summary>
	public void SetLockout(System.String userName,System.Boolean lockout,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Adds a claim to the specified user account
	/// </summary>
	public void AddClaim(System.String userName,SanteDB.Core.Security.Claims.IClaim claim,System.Security.Principal.IPrincipal principal,System.Nullable<System.TimeSpan> expiriy){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes a claim from the specified user account
	/// </summary>
	public void RemoveClaim(System.String userName,System.String claimType,System.Security.Principal.IPrincipal principal){
		throw new System.NotImplementedException();
	}
}
```

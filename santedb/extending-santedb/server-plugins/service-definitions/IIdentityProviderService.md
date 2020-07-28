---
description: IIdentityProviderService (SanteDB.Core.Api)
---

## Summary
Identity provider service

## Events

|Event|Type|Description|
|-|-|-|
|Authenticating|EventHandler&lt;AuthenticatingEventArgs>|Fired prior to an authentication event|
|Authenticated|EventHandler&lt;AuthenticatedEventArgs>|Fired after an authentication decision being made|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetIdentity|IIdentity|userName <small style='border:solid 1px #aaa'>String</small>|Retrieves an identity from the object|
|GetIdentity|IIdentity|sid <small style='border:solid 1px #aaa'>Guid</small>|Retrieves an identity from the object|
|CreateIdentity|IIdentity|userName <small style='border:solid 1px #aaa'>String</small><br/>password <small style='border:solid 1px #aaa'>String</small><br/>principal <small style='border:solid 1px #aaa'>IPrincipal</small>|Create a basic identity in the provider|
|Authenticate|IPrincipal|userName <small style='border:solid 1px #aaa'>String</small><br/>password <small style='border:solid 1px #aaa'>String</small>|Authenticate the user creating an identity|
|Authenticate|IPrincipal|userName <small style='border:solid 1px #aaa'>String</small><br/>password <small style='border:solid 1px #aaa'>String</small><br/>tfaSecret <small style='border:solid 1px #aaa'>String</small>|Authenticate the user creating an identity|
|ReAuthenticate|IPrincipal|principal <small style='border:solid 1px #aaa'>IPrincipal</small>|Perform a re-authentication of the principal|
|ChangePassword|void|userName <small style='border:solid 1px #aaa'>String</small><br/>newPassword <small style='border:solid 1px #aaa'>String</small><br/>principal <small style='border:solid 1px #aaa'>IPrincipal</small>|Change user password|
|GenerateTfaSecret|String|userName <small style='border:solid 1px #aaa'>String</small>|Set the user's two factor authentication secret|
|DeleteIdentity|void|userName <small style='border:solid 1px #aaa'>String</small><br/>principal <small style='border:solid 1px #aaa'>IPrincipal</small>|Delete an identity|
|SetLockout|void|userName <small style='border:solid 1px #aaa'>String</small><br/>lockout <small style='border:solid 1px #aaa'>Boolean</small><br/>principal <small style='border:solid 1px #aaa'>IPrincipal</small>|Set lockout|
|AddClaim|void|userName <small style='border:solid 1px #aaa'>String</small><br/>claim <small style='border:solid 1px #aaa'>IClaim</small><br/>principal <small style='border:solid 1px #aaa'>IPrincipal</small><br/>expiriy <small style='border:solid 1px #aaa'>Nullable<TimeSpan></small>|Adds a claim to the specified user account|
|RemoveClaim|void|userName <small style='border:solid 1px #aaa'>String</small><br/>claimType <small style='border:solid 1px #aaa'>String</small><br/>principal <small style='border:solid 1px #aaa'>IPrincipal</small>|Removes a claim from the specified user account|

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
	public event EventHandler<AuthenticatingEventArgs> Authenticating;
	/// <summary>
	/// Fired after an authentication decision being made
	/// </summary>
	public event EventHandler<AuthenticatedEventArgs> Authenticated;
	/// <summary>
	/// Retrieves an identity from the object
	/// </summary>
	public IIdentity GetIdentity(String userName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Retrieves an identity from the object
	/// </summary>
	public IIdentity GetIdentity(Guid sid){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a basic identity in the provider
	/// </summary>
	public IIdentity CreateIdentity(String userName,String password,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Authenticate the user creating an identity
	/// </summary>
	public IPrincipal Authenticate(String userName,String password){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Authenticate the user creating an identity
	/// </summary>
	public IPrincipal Authenticate(String userName,String password,String tfaSecret){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Perform a re-authentication of the principal
	/// </summary>
	public IPrincipal ReAuthenticate(IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Change user password
	/// </summary>
	public void ChangePassword(String userName,String newPassword,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Set the user's two factor authentication secret
	/// </summary>
	public String GenerateTfaSecret(String userName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Delete an identity
	/// </summary>
	public void DeleteIdentity(String userName,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Set lockout
	/// </summary>
	public void SetLockout(String userName,Boolean lockout,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Adds a claim to the specified user account
	/// </summary>
	public void AddClaim(String userName,IClaim claim,IPrincipal principal,Nullable<TimeSpan> expiriy){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes a claim from the specified user account
	/// </summary>
	public void RemoveClaim(String userName,String claimType,IPrincipal principal){
		throw new System.NotImplementedException();
	}
}
```

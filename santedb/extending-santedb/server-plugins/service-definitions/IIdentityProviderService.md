---
description: IIdentityProviderService (SanteDB.Core.Api)
---

## Summary
Identity provider service

## Events

|Event|Type|Description|
|-|-|-|
|Authenticating|System.EventHandler<SanteDB.Core.Security.Services.AuthenticatingEventArgs>|Fired prior to an authentication event|
|Authenticated|System.EventHandler<SanteDB.Core.Security.Services.AuthenticatedEventArgs>|Fired after an authentication decision being made|

## Properties


## Methods


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

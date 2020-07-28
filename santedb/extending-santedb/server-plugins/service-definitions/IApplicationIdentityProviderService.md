---
description: IApplicationIdentityProviderService (SanteDB.Core.Api)
---

## Summary
Represents a service which retrieves IPrincipal objects for applications.

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

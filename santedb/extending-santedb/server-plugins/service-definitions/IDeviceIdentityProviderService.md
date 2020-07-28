---
description: IDeviceIdentityProviderService (SanteDB.Core.Api)
---

## Summary
Represents an identity service which authenticates devices.

## Implementations


### ADO.NET Device Identity Provider - (SanteDB.Persistence.Data.ADO)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoDeviceIdentityProvider, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyDeviceIdentityProviderService : SanteDB.Core.Security.Services.IDeviceIdentityProviderService { 
	public String ServiceName => "My own IDeviceIdentityProviderService service";
	/// <summary>
	/// Fired after an authentication request has been made.
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Security.Services.AuthenticatedEventArgs> Authenticated;
	/// <summary>
	/// Fired prior to an authentication request being made.
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Security.Services.AuthenticatingEventArgs> Authenticating;
	/// <summary>
	/// Authenticates the specified device identifier.
	/// </summary>
	public System.Security.Principal.IPrincipal Authenticate(System.String deviceId,System.String deviceSecret,SanteDB.Core.Security.Services.AuthenticationMethod authMethod){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified identity for an device.
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
	/// Change the device secret
	/// </summary>
	public void ChangeSecret(System.String name,System.String deviceSecret,System.Security.Principal.IPrincipal systemPrincipal){
		throw new System.NotImplementedException();
	}
}
```

---
description: Device Identity Provider (IDeviceIdentityProviderService in SanteDB.Core.Api)
---

# Summary
Represents an identity service which authenticates devices.

# Events

|Event|Type|Description|
|-|-|-|
|Authenticated|EventHandler&lt;AuthenticatedEventArgs>|Fired after an authentication request has been made.|
|Authenticating|EventHandler&lt;AuthenticatingEventArgs>|Fired prior to an authentication request being made.|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Authenticate|IPrincipal|*String* **deviceId**<br/>*String* **deviceSecret**<br/>*AuthenticationMethod* **authMethod**|Authenticates the specified device identifier.|
|GetIdentity|IIdentity|*String* **name**|Gets the specified identity for an device.|
|SetLockout|void|*String* **name**<br/>*Boolean* **lockoutState**<br/>*IPrincipal* **principal**|Set the lockout status|
|ChangeSecret|void|*String* **name**<br/>*String* **deviceSecret**<br/>*IPrincipal* **systemPrincipal**|Change the device secret|

# Implementations


## ADO.NET Device Identity Provider - (SanteDB.Persistence.Data.ADO)
Represents a device identity provider.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoDeviceIdentityProvider, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyDeviceIdentityProviderService : SanteDB.Core.Security.Services.IDeviceIdentityProviderService { 
	public String ServiceName => "My own IDeviceIdentityProviderService service";
	/// <summary>
	/// Fired after an authentication request has been made.
	/// </summary>
	public event EventHandler<AuthenticatedEventArgs> Authenticated;
	/// <summary>
	/// Fired prior to an authentication request being made.
	/// </summary>
	public event EventHandler<AuthenticatingEventArgs> Authenticating;
	/// <summary>
	/// Authenticates the specified device identifier.
	/// </summary>
	public IPrincipal Authenticate(String deviceId,String deviceSecret,AuthenticationMethod authMethod){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified identity for an device.
	/// </summary>
	public IIdentity GetIdentity(String name){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Set the lockout status
	/// </summary>
	public void SetLockout(String name,Boolean lockoutState,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Change the device secret
	/// </summary>
	public void ChangeSecret(String name,String deviceSecret,IPrincipal systemPrincipal){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDeviceIdentityProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IDeviceIdentityProviderService.htm)
* [AdoDeviceIdentityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoDeviceIdentityProvider.htm)

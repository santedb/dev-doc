`IDeviceIdentityProviderService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a service which retrieves [IDeviceIdentity](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Principal_IDeviceIdentity.htm) and can authenticate to an [IPrincipal](https://docs.microsoft.com/en-us/dotnet/api/system.security.principal.iprincipal) for devices.

## Description
In SanteDB, a security session is comprised of up to three security identities/principals:

* (Optional) User identity representing the human using the application
* (Optional) A [IDeviceIdentity](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Principal_IDeviceIdentity.htm) representing the device running the application, and
* An [IApplicationIdentity](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Principal_IApplicationIdentity.htm) representing the application


This service is what is used to authenticate the device identity from a central credential store of registered devices. This service may be 
            called with a shared device id/secret (like a user name and password), or may be called with a device ID and x509 certificate (if used for authenticating
            sessions with a client certificate)

See: [SanteDB authentication architecture](https://help.santesuite.org/santedb/security-architecture#principals-and-identities)

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
|ChangeSecret|void|*String* **name**<br/>*String* **deviceSecret**<br/>*IPrincipal* **principal**|Change the device secret|

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
	public void ChangeSecret(String name,String deviceSecret,IPrincipal principal){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDeviceIdentityProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IDeviceIdentityProviderService.htm)
* [AdoDeviceIdentityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoDeviceIdentityProvider.htm)

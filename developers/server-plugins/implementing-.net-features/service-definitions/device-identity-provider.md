`IDeviceIdentityProviderService` in assembly SanteDB.Core.Api version 3.0.1980.0

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
|Authenticate|IPrincipal|*String* **deviceName**<br/>*String* **deviceSecret**<br/>*AuthenticationMethod* **authMethod**|Authenticates the specified device identifier.|
|CreateIdentity|IDeviceIdentity|*String* **deviceName**<br/>*String* **secret**<br/>*IPrincipal* **principal**<br/>*Nullable&lt;Guid>* **withSid**|Create a basic identity in the provider|
|GetSid|Guid|*String* **deviceName**|Gets the SID for the specified identity|
|GetIdentity|IDeviceIdentity|*String* **deviceName**|Gets the specified identity for an device.|
|GetIdentity|IDeviceIdentity|*Guid* **sid**|Gets the specified identity for an device.|
|SetLockout|void|*String* **deviceName**<br/>*Boolean* **lockoutState**<br/>*IPrincipal* **principal**|Set the lockout status|
|ChangeSecret|void|*String* **deviceName**<br/>*String* **deviceSecret**<br/>*IPrincipal* **principal**|Change the device secret|
|AddClaim|void|*String* **deviceName**<br/>*IClaim* **claim**<br/>*IPrincipal* **principal**<br/>*Nullable&lt;TimeSpan>* **expiry**|Add a  to|
|GetClaims|IEnumerable&lt;IClaim>|*String* **deviceName**|Get all active claims for the specified device|
|RemoveClaim|void|*String* **deviceName**<br/>*String* **claimType**<br/>*IPrincipal* **principal**|Removes a claim from the specified device account|

# Implementations


## UpstreamDeviceIdentityProvider - (SanteDB.Client)
Represents an identity provider that provides upstream device identities
### Description
This is a partial implementation only for the resolution of identity objects

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Security.UpstreamDeviceIdentityProvider, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AdoDeviceIdentityProvider - (SanteDB.Persistence.Data)
An implementation of the device identity provider

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.AdoDeviceIdentityProvider, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
	public IPrincipal Authenticate(String deviceName,String deviceSecret,AuthenticationMethod authMethod){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a basic identity in the provider
	/// </summary>
	public IDeviceIdentity CreateIdentity(String deviceName,String secret,IPrincipal principal,Nullable<Guid> withSid){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the SID for the specified identity
	/// </summary>
	public Guid GetSid(String deviceName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified identity for an device.
	/// </summary>
	public IDeviceIdentity GetIdentity(String deviceName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified identity for an device.
	/// </summary>
	public IDeviceIdentity GetIdentity(Guid sid){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Set the lockout status
	/// </summary>
	public void SetLockout(String deviceName,Boolean lockoutState,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Change the device secret
	/// </summary>
	public void ChangeSecret(String deviceName,String deviceSecret,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Add a  to
	/// </summary>
	public void AddClaim(String deviceName,IClaim claim,IPrincipal principal,Nullable<TimeSpan> expiry){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all active claims for the specified device
	/// </summary>
	public IEnumerable<IClaim> GetClaims(String deviceName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes a claim from the specified device account
	/// </summary>
	public void RemoveClaim(String deviceName,String claimType,IPrincipal principal){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDeviceIdentityProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IDeviceIdentityProviderService.htm)
* [UpstreamDeviceIdentityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Security_UpstreamDeviceIdentityProvider.htm)
* [AdoDeviceIdentityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoDeviceIdentityProvider.htm)

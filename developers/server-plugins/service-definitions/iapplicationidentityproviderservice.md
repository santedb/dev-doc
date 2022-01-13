---
description: Application Identity Provider (IApplicationIdentityProviderService in SanteDB.Core.Api)
---

# Summary
Represents a service which retrieves [IApplicationIdentity](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Principal_IApplicationIdentity.htm) and can authenticate to an [IPrincipal](https://docs.microsoft.com/en-us/dotnet/api/system.security.principal.iprincipal) for applications.

## Description
In SanteDB, a security session is comprised of up to three security identities/principals:

* (Optional) User identity representing the human using the application
* (Optional) Device identity representing the device running the application, and
* An [IApplicationIdentity](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Principal_IApplicationIdentity.htm) representing the application


This service is what is used to authenticate the application identity from a central credential store of registered applications.

See: [SanteDB authentication architecture](https://help.santesuite.org/santedb/security-architecture#principals-and-identities)

# Events

|Event|Type|Description|
|-|-|-|
|Authenticated|EventHandler&lt;AuthenticatedEventArgs>|Fired after an authentication request has been made.|
|Authenticating|EventHandler&lt;AuthenticatingEventArgs>|Fired prior to an authentication request being made.|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Authenticate|IPrincipal|*String* **applicationId**<br/>*String* **applicationSecret**|Authenticate the application identity.|
|GetIdentity|IIdentity|*String* **name**|Gets the specified identity for an application.|
|SetLockout|void|*String* **name**<br/>*Boolean* **lockoutState**<br/>*IPrincipal* **principal**|Set the lockout status|
|ChangeSecret|void|*String* **name**<br/>*String* **secret**<br/>*IPrincipal* **principal**|Change the specified application identity's secret|
|GetSecureKey|Byte[]|*String* **name**|Get the secure key for the specified application (can be used for symmetric encryption)|

# Implementations


## ADO.NET Application Identity Provider - (SanteDB.Persistence.Data.ADO)
Sql Application IdP

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoApplicationIdentityProvider, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyApplicationIdentityProviderService : SanteDB.Core.Security.Services.IApplicationIdentityProviderService { 
	public String ServiceName => "My own IApplicationIdentityProviderService service";
	/// <summary>
	/// Fired after an authentication request has been made.
	/// </summary>
	public event EventHandler<AuthenticatedEventArgs> Authenticated;
	/// <summary>
	/// Fired prior to an authentication request being made.
	/// </summary>
	public event EventHandler<AuthenticatingEventArgs> Authenticating;
	/// <summary>
	/// Authenticate the application identity.
	/// </summary>
	public IPrincipal Authenticate(String applicationId,String applicationSecret){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified identity for an application.
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
	/// Change the specified application identity's secret
	/// </summary>
	public void ChangeSecret(String name,String secret,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the secure key for the specified application (can be used for symmetric encryption)
	/// </summary>
	public Byte[] GetSecureKey(String name){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IApplicationIdentityProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IApplicationIdentityProviderService.htm)
* [AdoApplicationIdentityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoApplicationIdentityProvider.htm)

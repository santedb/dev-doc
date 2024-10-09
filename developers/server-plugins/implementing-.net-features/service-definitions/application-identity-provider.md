`IApplicationIdentityProviderService` in assembly SanteDB.Core.Api version 3.0.1980.0

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
|Authenticate|IPrincipal|*String* **applicationName**<br/>*String* **applicationSecret**|Authenticate the application identity.|
|Authenticate|IPrincipal|*String* **applicationName**<br/>*IPrincipal* **authenticationContext**|Authenticate the application identity.|
|CreateIdentity|IApplicationIdentity|*String* **applicationName**<br/>*String* **password**<br/>*IPrincipal* **principal**<br/>*Nullable&lt;Guid>* **withSid**|Create a basic identity in the provider|
|GetIdentity|IApplicationIdentity|*String* **applicationName**|Gets the specified identity for an application.|
|GetIdentity|IApplicationIdentity|*Guid* **sid**|Gets the specified identity for an application.|
|GetSid|Guid|*String* **name**|Gets the SID for the specified identity|
|SetLockout|void|*String* **applicationName**<br/>*Boolean* **lockoutState**<br/>*IPrincipal* **principal**|Set the lockout status|
|ChangeSecret|void|*String* **applicationName**<br/>*String* **secret**<br/>*IPrincipal* **principal**|Change the specified application identity's secret|
|AddClaim|void|*String* **applicationName**<br/>*IClaim* **claim**<br/>*IPrincipal* **principal**<br/>*Nullable&lt;TimeSpan>* **expiry**|Add a  to|
|GetClaims|IEnumerable&lt;IClaim>|*String* **applicationName**|Get all active claims for the specified application|
|RemoveClaim|void|*String* **applicationName**<br/>*String* **claimType**<br/>*IPrincipal* **principal**|Removes a claim from the specified device account|

# Implementations


## BridgedApplicationIdentityProvider - (SanteDB.Client)
Application identity provider service that bridges between local and upstream

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Security.BridgedApplicationIdentityProvider, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## UpstreamApplicationIdentityProvider - (SanteDB.Client)
Represents an implementation of a [IApplicationIdentityProviderService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IApplicationIdentityProviderService.htm) which uses OAUTH

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Security.UpstreamApplicationIdentityProvider, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AdoApplicationIdentityProvider - (SanteDB.Persistence.Data)
Application identity provider that uses the database to authenticate applications

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.AdoApplicationIdentityProvider, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
	public IPrincipal Authenticate(String applicationName,String applicationSecret){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Authenticate the application identity.
	/// </summary>
	public IPrincipal Authenticate(String applicationName,IPrincipal authenticationContext){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Create a basic identity in the provider
	/// </summary>
	public IApplicationIdentity CreateIdentity(String applicationName,String password,IPrincipal principal,Nullable<Guid> withSid){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified identity for an application.
	/// </summary>
	public IApplicationIdentity GetIdentity(String applicationName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified identity for an application.
	/// </summary>
	public IApplicationIdentity GetIdentity(Guid sid){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the SID for the specified identity
	/// </summary>
	public Guid GetSid(String name){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Set the lockout status
	/// </summary>
	public void SetLockout(String applicationName,Boolean lockoutState,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Change the specified application identity's secret
	/// </summary>
	public void ChangeSecret(String applicationName,String secret,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Add a  to
	/// </summary>
	public void AddClaim(String applicationName,IClaim claim,IPrincipal principal,Nullable<TimeSpan> expiry){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all active claims for the specified application
	/// </summary>
	public IEnumerable<IClaim> GetClaims(String applicationName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes a claim from the specified device account
	/// </summary>
	public void RemoveClaim(String applicationName,String claimType,IPrincipal principal){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IApplicationIdentityProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IApplicationIdentityProviderService.htm)
* [BridgedApplicationIdentityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Security_BridgedApplicationIdentityProvider.htm)
* [UpstreamApplicationIdentityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Security_UpstreamApplicationIdentityProvider.htm)
* [AdoApplicationIdentityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoApplicationIdentityProvider.htm)

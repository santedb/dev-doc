---
description: User Identity Provider (IIdentityProviderService in SanteDB.Core.Api)
---

# Summary
Identity provider service

# Events

|Event|Type|Description|
|-|-|-|
|Authenticating|EventHandler&lt;AuthenticatingEventArgs>|Fired prior to an authentication event|
|Authenticated|EventHandler&lt;AuthenticatedEventArgs>|Fired after an authentication decision being made|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetIdentity|IIdentity|*String* **userName**|Retrieves an identity from the object|
|GetIdentity|IIdentity|*Guid* **sid**|Retrieves an identity from the object|
|CreateIdentity|IIdentity|*String* **userName**<br/>*String* **password**<br/>*IPrincipal* **principal**|Create a basic identity in the provider|
|Authenticate|IPrincipal|*String* **userName**<br/>*String* **password**|Authenticate the user creating an identity|
|Authenticate|IPrincipal|*String* **userName**<br/>*String* **password**<br/>*String* **tfaSecret**|Authenticate the user creating an identity|
|ReAuthenticate|IPrincipal|*IPrincipal* **principal**|Perform a re-authentication of the principal|
|ChangePassword|void|*String* **userName**<br/>*String* **newPassword**<br/>*IPrincipal* **principal**|Change user password|
|DeleteIdentity|void|*String* **userName**<br/>*IPrincipal* **principal**|Delete an identity|
|SetLockout|void|*String* **userName**<br/>*Boolean* **lockout**<br/>*IPrincipal* **principal**|Set lockout|
|AddClaim|void|*String* **userName**<br/>*IClaim* **claim**<br/>*IPrincipal* **principal**<br/>*Nullable&lt;TimeSpan>* **expiriy**|Adds a claim to the specified user account|
|RemoveClaim|void|*String* **userName**<br/>*String* **claimType**<br/>*IPrincipal* **principal**|Removes a claim from the specified user account|

# Implementations


## ADO.NET Identity Provider - (SanteDB.Persistence.Data.ADO)
Identity provider service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoIdentityProvider, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
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

# References

* [IIdentityProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IIdentityProviderService.htm)
* [AdoIdentityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoIdentityProvider.htm)

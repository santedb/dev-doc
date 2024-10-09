`IIdentityProviderService` in assembly SanteDB.Core.Api version 3.0.1980.0

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
|CreateIdentity|IIdentity|*String* **userName**<br/>*String* **password**<br/>*IPrincipal* **principal**<br/>*Nullable&lt;Guid>* **withSid**|Create a basic identity in the provider|
|Authenticate|IPrincipal|*String* **userName**<br/>*String* **password**<br/>*IEnumerable&lt;IClaim>* **clientClaimAssertions**<br/>*IEnumerable&lt;String>* **demandedScopes**|Authenticate the user creating an identity|
|Authenticate|IPrincipal|*String* **userName**<br/>*String* **password**<br/>*String* **tfaSecret**<br/>*IEnumerable&lt;IClaim>* **clientClaimAssertions**<br/>*IEnumerable&lt;String>* **demandedScopes**|Authenticate the user creating an identity|
|ReAuthenticate|IPrincipal|*IPrincipal* **principal**|Recheck the authentication of an already authenticated .|
|ChangePassword|void|*String* **userName**<br/>*String* **newPassword**<br/>*IPrincipal* **principal**<br/>*Boolean* **isSynchronizationOperation**|Change user password|
|DeleteIdentity|void|*String* **userName**<br/>*IPrincipal* **principal**|Delete an identity|
|SetLockout|void|*String* **userName**<br/>*Boolean* **lockout**<br/>*IPrincipal* **principal**|Set lockout|
|AddClaim|void|*String* **userName**<br/>*IClaim* **claim**<br/>*IPrincipal* **principal**<br/>*Nullable&lt;TimeSpan>* **expiry**|Adds a claim to the specified user account|
|RemoveClaim|void|*String* **userName**<br/>*String* **claimType**<br/>*IPrincipal* **principal**|Removes a claim from the specified user account|
|GetClaims|IEnumerable&lt;IClaim>|*String* **userName**|Get all active claims for the specified user|
|GetSid|Guid|*String* **userName**|Get the SID for the named user|
|GetAuthenticationMethods|AuthenticationMethod|*String* **userName**|Gets the applicable authentication methods from the identity provider for|
|ExpirePassword|void|*String* **userName**<br/>*IPrincipal* **principal**|Indicates that the password for the  should be immediately expired (user must change password at next login)|

# Implementations


## BridgedIdentityProvider - (SanteDB.Client)
Represents an identity provider which bridges local and upstream

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Security.BridgedIdentityProvider, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## UpstreamIdentityProvider - (SanteDB.Client)
Represents an implementation of the [IIdentityProviderService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IIdentityProviderService.htm) which uses an upstream oauth server

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Security.UpstreamIdentityProvider, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AdoIdentityProvider - (SanteDB.Persistence.Data)
An identity provider implemented for .NET

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.AdoIdentityProvider, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
	public IIdentity CreateIdentity(String userName,String password,IPrincipal principal,Nullable<Guid> withSid){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Authenticate the user creating an identity
	/// </summary>
	public IPrincipal Authenticate(String userName,String password,IEnumerable<IClaim> clientClaimAssertions,IEnumerable<String> demandedScopes){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Authenticate the user creating an identity
	/// </summary>
	public IPrincipal Authenticate(String userName,String password,String tfaSecret,IEnumerable<IClaim> clientClaimAssertions,IEnumerable<String> demandedScopes){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Recheck the authentication of an already authenticated .
	/// </summary>
	public IPrincipal ReAuthenticate(IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Change user password
	/// </summary>
	public void ChangePassword(String userName,String newPassword,IPrincipal principal,Boolean isSynchronizationOperation){
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
	public void AddClaim(String userName,IClaim claim,IPrincipal principal,Nullable<TimeSpan> expiry){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes a claim from the specified user account
	/// </summary>
	public void RemoveClaim(String userName,String claimType,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get all active claims for the specified user
	/// </summary>
	public IEnumerable<IClaim> GetClaims(String userName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the SID for the named user
	/// </summary>
	public Guid GetSid(String userName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the applicable authentication methods from the identity provider for
	/// </summary>
	public AuthenticationMethod GetAuthenticationMethods(String userName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Indicates that the password for the  should be immediately expired (user must change password at next login)
	/// </summary>
	public void ExpirePassword(String userName,IPrincipal principal){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IIdentityProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IIdentityProviderService.htm)
* [BridgedIdentityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Security_BridgedIdentityProvider.htm)
* [UpstreamIdentityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Security_UpstreamIdentityProvider.htm)
* [AdoIdentityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoIdentityProvider.htm)

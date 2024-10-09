`ISecurityChallengeIdentityService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a security challenge service which can provide identity

# Events

|Event|Type|Description|
|-|-|-|
|Authenticating|EventHandler&lt;AuthenticatingEventArgs>|Fired prior to an authentication event|
|Authenticated|EventHandler&lt;AuthenticatedEventArgs>|Fired after an authentication decision being made|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Authenticate|IPrincipal|*String* **userName**<br/>*Guid* **challengeKey**<br/>*String* **response**<br/>*String* **tfaSecret**|Authenticates the specified user with a challenge key and response|

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

## AdoSecurityChallengeProvider - (SanteDB.Persistence.Data)
Represents a callenge service which uses the ADO.NET tables

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.AdoSecurityChallengeProvider, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MySecurityChallengeIdentityService : SanteDB.Core.Security.Services.ISecurityChallengeIdentityService { 
	public String ServiceName => "My own ISecurityChallengeIdentityService service";
	/// <summary>
	/// Fired prior to an authentication event
	/// </summary>
	public event EventHandler<AuthenticatingEventArgs> Authenticating;
	/// <summary>
	/// Fired after an authentication decision being made
	/// </summary>
	public event EventHandler<AuthenticatedEventArgs> Authenticated;
	/// <summary>
	/// Authenticates the specified user with a challenge key and response
	/// </summary>
	public IPrincipal Authenticate(String userName,Guid challengeKey,String response,String tfaSecret){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ISecurityChallengeIdentityService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_ISecurityChallengeIdentityService.htm)
* [BridgedIdentityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Security_BridgedIdentityProvider.htm)
* [UpstreamIdentityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Security_UpstreamIdentityProvider.htm)
* [AdoSecurityChallengeProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoSecurityChallengeProvider.htm)

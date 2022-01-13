Security Challenge Authentication Provider (ISecurityChallengeIdentityService in SanteDB.Core.Api)

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


## AdoSecurityChallengeProvider - (SanteDB.Persistence.Data.ADO)
Represents a callenge service which uses the ADO.NET tables

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoSecurityChallengeProvider, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security;
/// Other usings here
public class MySecurityChallengeIdentityService : SanteDB.Core.Security.ISecurityChallengeIdentityService { 
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

* [ISecurityChallengeIdentityService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_ISecurityChallengeIdentityService.htm)
* [AdoSecurityChallengeProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoSecurityChallengeProvider.htm)

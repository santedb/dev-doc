`ISecurityChallengeService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents an interface that allows for the retrieval of pre-configured security challenges

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Get|IEnumerable&lt;SecurityChallenge>|*String* **userName**<br/>*IPrincipal* **principal**|Gets the challenges current registered for the user (not the answers)|
|Get|IEnumerable&lt;SecurityChallenge>|*Guid* **userKey**<br/>*IPrincipal* **principal**|Gets the challenges current registered for the user (not the answers)|
|Set|void|*String* **userName**<br/>*Guid* **challengeKey**<br/>*String* **response**<br/>*IPrincipal* **principal**|Add a challenge to the current registered user|
|Remove|void|*String* **userName**<br/>*Guid* **challengeKey**<br/>*IPrincipal* **principal**|Removes or clears the specified challenge|

# Implementations


## UpstreamSecurityChallengeProvider - (SanteDB.Client)
Remote security challenge provider repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Repositories.UpstreamSecurityChallengeProvider, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
public class MySecurityChallengeService : SanteDB.Core.Security.Services.ISecurityChallengeService { 
	public String ServiceName => "My own ISecurityChallengeService service";
	/// <summary>
	/// Gets the challenges current registered for the user (not the answers)
	/// </summary>
	public IEnumerable<SecurityChallenge> Get(String userName,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the challenges current registered for the user (not the answers)
	/// </summary>
	public IEnumerable<SecurityChallenge> Get(Guid userKey,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Add a challenge to the current registered user
	/// </summary>
	public void Set(String userName,Guid challengeKey,String response,IPrincipal principal){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Removes or clears the specified challenge
	/// </summary>
	public void Remove(String userName,Guid challengeKey,IPrincipal principal){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ISecurityChallengeService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_ISecurityChallengeService.htm)
* [UpstreamSecurityChallengeProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Repositories_UpstreamSecurityChallengeProvider.htm)
* [AdoSecurityChallengeProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoSecurityChallengeProvider.htm)

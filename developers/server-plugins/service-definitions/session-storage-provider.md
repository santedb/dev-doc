Session Storage Provider (ISessionProviderService in SanteDB.Core.Api)

# Summary
Represents a service which is responsible for the storage and retrieval of sessions

# Events

|Event|Type|Description|
|-|-|-|
|Established|EventHandler&lt;SessionEstablishedEventArgs>|Fired when the session provider service has established|
|Abandoned|EventHandler&lt;SessionEstablishedEventArgs>|Fired when the session provider service has ended by the user's decision|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Establish|ISession|*IPrincipal* **principal**<br/>*String* **remoteEp**<br/>*Boolean* **isOverride**<br/>*String* **purpose**<br/>*String[]* **scope**<br/>*String* **lang**|Establishes a session for the specified principal|
|Get|ISession|*Byte[]* **sessionToken**<br/>*Boolean* **allowExpired**|Authenticates the session identifier as evidence of session|
|Extend|ISession|*Byte[]* **refreshToken**|Extend the session with the specified refresh token|
|Abandon|void|*ISession* **session**|Abandons the session|

# Implementations


## ADO.NET Session Storage - (SanteDB.Persistence.Data.ADO)
Represents a session provider for ADO based sessions

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoSessionProvider, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MySessionProviderService : SanteDB.Core.Services.ISessionProviderService { 
	public String ServiceName => "My own ISessionProviderService service";
	/// <summary>
	/// Fired when the session provider service has established
	/// </summary>
	public event EventHandler<SessionEstablishedEventArgs> Established;
	/// <summary>
	/// Fired when the session provider service has ended by the user's decision
	/// </summary>
	public event EventHandler<SessionEstablishedEventArgs> Abandoned;
	/// <summary>
	/// Establishes a session for the specified principal
	/// </summary>
	public ISession Establish(IPrincipal principal,String remoteEp,Boolean isOverride,String purpose,String[] scope,String lang){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Authenticates the session identifier as evidence of session
	/// </summary>
	public ISession Get(Byte[] sessionToken,Boolean allowExpired){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Extend the session with the specified refresh token
	/// </summary>
	public ISession Extend(Byte[] refreshToken){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Abandons the session
	/// </summary>
	public void Abandon(ISession session){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ISessionProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ISessionProviderService.htm)
* [AdoSessionProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoSessionProvider.htm)

`ISessionProviderService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a service which is responsible for the storage and retrieval of sessions

# Events

|Event|Type|Description|
|-|-|-|
|Established|EventHandler&lt;SessionEstablishedEventArgs>|Fired when the session provider service has established|
|Abandoned|EventHandler&lt;SessionEstablishedEventArgs>|Fired when the session provider service has ended by the user's decision|
|Extended|EventHandler&lt;SessionEstablishedEventArgs>|Fired when the session provider service has been extended|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Establish|ISession|*IPrincipal* **principal**<br/>*String* **remoteEp**<br/>*Boolean* **isOverride**<br/>*String* **purpose**<br/>*String[]* **scope**<br/>*String* **lang**|Establishes a session for the specified principal|
|Get|ISession|*Byte[]* **sessionId**<br/>*Boolean* **allowExpired**|Authenticates the session identifier as evidence of session|
|GetUserSessions|ISession[]|*Guid* **userKey**|Gets active sessions for the user.|
|Extend|ISession|*Byte[]* **refreshToken**|Extend the session with the specified refresh token|
|Abandon|void|*ISession* **session**|Abandons the session|
|GetActiveSessions|ISession[]|*none*|TODO|

# Implementations


## MemorySessionManagerService - (SanteDB.Caching.Memory)
Represents a [ISessionProviderService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_ISessionProviderService.htm) which uses RAM caching

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Caching.Memory.Session.MemorySessionManagerService, SanteDB.Caching.Memory, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## BridgedSessionManager - (SanteDB.Client)
Represents a bridged session provider manager
### Description
This class is responsible for managing local sessions (via a synchronized pattern) as well as upstream sessions which need to 
            interact with the upstream, as well as transitioning between the two.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Security.BridgedSessionManager, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AdoSessionProvider - (SanteDB.Persistence.Data)
An identity provider service that uses the ADO session table

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.AdoSessionProvider, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MySessionProviderService : SanteDB.Core.Security.Services.ISessionProviderService { 
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
	/// Fired when the session provider service has been extended
	/// </summary>
	public event EventHandler<SessionEstablishedEventArgs> Extended;
	/// <summary>
	/// Establishes a session for the specified principal
	/// </summary>
	public ISession Establish(IPrincipal principal,String remoteEp,Boolean isOverride,String purpose,String[] scope,String lang){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Authenticates the session identifier as evidence of session
	/// </summary>
	public ISession Get(Byte[] sessionId,Boolean allowExpired){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets active sessions for the user.
	/// </summary>
	public ISession[] GetUserSessions(Guid userKey){
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
	public ISession[] GetActiveSessions(){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ISessionProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_ISessionProviderService.htm)
* [MemorySessionManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Memory_Session_MemorySessionManagerService.htm)
* [BridgedSessionManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Security_BridgedSessionManager.htm)
* [AdoSessionProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoSessionProvider.htm)

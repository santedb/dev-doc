`ISessionIdentityProviderService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a session identity service that can provide identities

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Authenticate|IPrincipal|*ISession* **session**|Authenticate based on session|
|GetIdentities|IIdentity[]|*ISession* **session**|Gets an un-authenticated principal from the specified session|

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
public class MySessionIdentityProviderService : SanteDB.Core.Security.Services.ISessionIdentityProviderService { 
	public String ServiceName => "My own ISessionIdentityProviderService service";
	/// <summary>
	/// Authenticate based on session
	/// </summary>
	public IPrincipal Authenticate(ISession session){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets an un-authenticated principal from the specified session
	/// </summary>
	public IIdentity[] GetIdentities(ISession session){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ISessionIdentityProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_ISessionIdentityProviderService.htm)
* [MemorySessionManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Caching_Memory_Session_MemorySessionManagerService.htm)
* [BridgedSessionManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Security_BridgedSessionManager.htm)
* [AdoSessionProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoSessionProvider.htm)

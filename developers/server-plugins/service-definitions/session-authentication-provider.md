---
description: Session Authentication Provider (ISessionIdentityProviderService in SanteDB.Core.Api)
---

# Summary
Represents a session identity service that can provide identities

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Authenticate|IPrincipal|*ISession* **session**|Authenticate based on session|
|GetIdentities|IIdentity[]|*ISession* **session**|Gets an un-authenticated principal from the specified session|

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
using SanteDB.Core.Services;
/// Other usings here
public class MySessionIdentityProviderService : SanteDB.Core.Services.ISessionIdentityProviderService { 
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

* [ISessionIdentityProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ISessionIdentityProviderService.htm)
* [AdoIdentityProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoIdentityProvider.htm)

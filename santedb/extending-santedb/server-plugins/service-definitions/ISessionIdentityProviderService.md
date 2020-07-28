---
description: ISessionIdentityProviderService (SanteDB.Core.Api)
---

## Summary
Represents a session identity service that can provide identities

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Authenticate|IPrincipal|*ISession* **session**|Authenticate based on session|
|GetIdentities|IIdentity[]|*ISession* **session**|Gets an un-authenticated principal from the specified session|

## Implementations


### ADO.NET Identity Provider - (SanteDB.Persistence.Data.ADO)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoIdentityProvider, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
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

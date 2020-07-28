---
description: ISessionProviderService (SanteDB.Core.Api)
---

## Summary
Represents a service which is responsible for the storage and retrieval of sessions

## Events

|Event|Type|Description|
|-|-|-|
|Established|System.EventHandler&lt;SanteDB.Core.Services.SessionEstablishedEventArgs>|Fired when the session provider service has established|
|Abandoned|System.EventHandler&lt;SanteDB.Core.Services.SessionEstablishedEventArgs>|Fired when the session provider service has ended by the user's decision|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Establish|SanteDB.Core.Security.ISession|principal <small style='border:solid 1px #aaa'>System.Security.Principal.IPrincipal</small><br/>remoteEp <small style='border:solid 1px #aaa'>System.String</small><br/>isOverride <small style='border:solid 1px #aaa'>System.Boolean</small><br/>purpose <small style='border:solid 1px #aaa'>System.String</small><br/>scope <small style='border:solid 1px #aaa'>System.String[]</small><br/>lang <small style='border:solid 1px #aaa'>System.String</small>|Establishes a session for the specified principal|
|Get|SanteDB.Core.Security.ISession|sessionToken <small style='border:solid 1px #aaa'>System.Byte[]</small><br/>allowExpired <small style='border:solid 1px #aaa'>System.Boolean</small>|Authenticates the session identifier as evidence of session|
|Extend|SanteDB.Core.Security.ISession|refreshToken <small style='border:solid 1px #aaa'>System.Byte[]</small>|Extend the session with the specified refresh token|
|Abandon|void|session <small style='border:solid 1px #aaa'>SanteDB.Core.Security.ISession</small>|Abandons the session|

## Implementations


### ADO.NET Session Storage - (SanteDB.Persistence.Data.ADO)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoSessionProvider, SanteDB.Persistence.Data.ADO, Version=2.0.27.29202, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MySessionProviderService : SanteDB.Core.Services.ISessionProviderService { 
	public String ServiceName => "My own ISessionProviderService service";
	/// <summary>
	/// Fired when the session provider service has established
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Services.SessionEstablishedEventArgs> Established;
	/// <summary>
	/// Fired when the session provider service has ended by the user's decision
	/// </summary>
	public event System.EventHandler<SanteDB.Core.Services.SessionEstablishedEventArgs> Abandoned;
	/// <summary>
	/// Establishes a session for the specified principal
	/// </summary>
	public SanteDB.Core.Security.ISession Establish(System.Security.Principal.IPrincipal principal,System.String remoteEp,System.Boolean isOverride,System.String purpose,System.String[] scope,System.String lang){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Authenticates the session identifier as evidence of session
	/// </summary>
	public SanteDB.Core.Security.ISession Get(System.Byte[] sessionToken,System.Boolean allowExpired){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Extend the session with the specified refresh token
	/// </summary>
	public SanteDB.Core.Security.ISession Extend(System.Byte[] refreshToken){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Abandons the session
	/// </summary>
	public void Abandon(SanteDB.Core.Security.ISession session){
		throw new System.NotImplementedException();
	}
}
```

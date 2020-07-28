---
description: INetworkInformationService (SanteDB.Core.Api)
---

## Summary
Represents network information service

## Events

|Event|Type|Description|
|-|-|-|
|NetworkStatusChanged|System.EventHandler|Fired when the network status changes|

## Properties


## Methods


## Implementations


### Default Network Information Service - (SanteDB.Core)
Default network information service

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.DefaultNetworkInformationService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyNetworkInformationService : SanteDB.Core.Services.INetworkInformationService { 
	public String ServiceName => "My own INetworkInformationService service";
	/// <summary>
	/// Fired when the network status changes
	/// </summary>
	public event System.EventHandler NetworkStatusChanged;
	/// <summary>
	/// Gets whether the network is available
	/// </summary>
	public System.Boolean IsNetworkAvailable {
		get;
	}
	/// <summary>
	/// Gets whether the network is connected.
	/// </summary>
	public System.Boolean IsNetworkConnected {
		get;
	}
	/// <summary>
	/// Returns true if the network is WIFI
	/// </summary>
	public System.Boolean IsNetworkWifi {
		get;
	}
	public System.Collections.Generic.IEnumerable<SanteDB.Core.Services.NetworkInterfaceInfo> GetInterfaces(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Pings the specified host
	/// </summary>
	public System.Int64 Ping(System.String hostName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Perform a DNS lookup
	/// </summary>
	public System.String Nslookup(System.String address){
		throw new System.NotImplementedException();
	}
	public System.String GetHostName(){
		throw new System.NotImplementedException();
	}
	public System.String GetMachineName(){
		throw new System.NotImplementedException();
	}
}
```

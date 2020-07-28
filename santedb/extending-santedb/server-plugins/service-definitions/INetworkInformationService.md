---
description: INetworkInformationService (SanteDB.Core.Api)
---

## Summary
Represents network information service

## Events

|Event|Type|Description|
|-|-|-|
|NetworkStatusChanged|EventHandler|Fired when the network status changes|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|
|IsNetworkAvailable|Boolean|R|Gets whether the network is available|
|IsNetworkConnected|Boolean|R|Gets whether the network is connected.|
|IsNetworkWifi|Boolean|R|Returns true if the network is WIFI|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetInterfaces|IEnumerable&lt;NetworkInterfaceInfo>||TODO|
|Ping|Int64|hostName <small style='border:solid 1px #aaa'>String</small>|Pings the specified host|
|Nslookup|String|address <small style='border:solid 1px #aaa'>String</small>|Perform a DNS lookup|
|GetHostName|String||TODO|
|GetMachineName|String||TODO|

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
	public event EventHandler NetworkStatusChanged;
	/// <summary>
	/// Gets whether the network is available
	/// </summary>
	public Boolean IsNetworkAvailable {
		get;
	}
	/// <summary>
	/// Gets whether the network is connected.
	/// </summary>
	public Boolean IsNetworkConnected {
		get;
	}
	/// <summary>
	/// Returns true if the network is WIFI
	/// </summary>
	public Boolean IsNetworkWifi {
		get;
	}
	public IEnumerable<NetworkInterfaceInfo> GetInterfaces(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Pings the specified host
	/// </summary>
	public Int64 Ping(String hostName){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Perform a DNS lookup
	/// </summary>
	public String Nslookup(String address){
		throw new System.NotImplementedException();
	}
	public String GetHostName(){
		throw new System.NotImplementedException();
	}
	public String GetMachineName(){
		throw new System.NotImplementedException();
	}
}
```

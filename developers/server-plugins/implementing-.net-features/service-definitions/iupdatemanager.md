`IUpdateManager` in assembly SanteDB.Client version 3.0.1980.0

# Summary
Update manager service is responsible for checking for updates and downloading / applying them

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetServerInfo|AppletInfo|*String* **packageId**|Get server version of a package|
|Install|void|*String* **packageId**|Install the specified package from the server version|
|Update|void|*Boolean* **nonInteractive**|Update all apps|

# Implementations


## UpstreamUpdateManagerService - (SanteDB.Client)
Update manager which uses the AMI to get updates for packages

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.UpstreamUpdateManagerService, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Client.Services;
/// Other usings here
public class MyUpdateManager : SanteDB.Client.Services.IUpdateManager { 
	public String ServiceName => "My own IUpdateManager service";
	/// <summary>
	/// Get server version of a package
	/// </summary>
	public AppletInfo GetServerInfo(String packageId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Install the specified package from the server version
	/// </summary>
	public void Install(String packageId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Update all apps
	/// </summary>
	public void Update(Boolean nonInteractive){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IUpdateManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Services_IUpdateManager.htm)
* [UpstreamUpdateManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_UpstreamUpdateManagerService.htm)

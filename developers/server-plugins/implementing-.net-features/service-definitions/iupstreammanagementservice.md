`IUpstreamManagementService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents an upstream enrolment management service

# Events

|Event|Type|Description|
|-|-|-|
|RealmChanging|EventHandler&lt;UpstreamRealmChangedEventArgs>|The realm settings are changing but not committed.|
|RealmChanged|EventHandler&lt;UpstreamRealmChangedEventArgs>|The realm settings have changed|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Join|void|*IUpstreamRealmSettings* **targetRealm**<br/>*Boolean* **replaceExistingRegistration**<br/>*String&* **welcomeMessage**|Joins the specified|
|IsConfigured|Boolean|*none*|TODO|
|GetSettings|IUpstreamRealmSettings|*none*|TODO|
|UnJoin|void|*none*|TODO|

# Implementations


## Upstream Management - (SanteDB.Client)
An upstream management service which manages the upstream

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Management.DefaultUpstreamManagementService, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyUpstreamManagementService : SanteDB.Core.Services.IUpstreamManagementService { 
	public String ServiceName => "My own IUpstreamManagementService service";
	/// <summary>
	/// The realm settings are changing but not committed.
	/// </summary>
	public event EventHandler<UpstreamRealmChangedEventArgs> RealmChanging;
	/// <summary>
	/// The realm settings have changed
	/// </summary>
	public event EventHandler<UpstreamRealmChangedEventArgs> RealmChanged;
	/// <summary>
	/// Joins the specified
	/// </summary>
	public void Join(IUpstreamRealmSettings targetRealm,Boolean replaceExistingRegistration,String& welcomeMessage){
		throw new System.NotImplementedException();
	}
	public Boolean IsConfigured(){
		throw new System.NotImplementedException();
	}
	public IUpstreamRealmSettings GetSettings(){
		throw new System.NotImplementedException();
	}
	public void UnJoin(){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IUpstreamManagementService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IUpstreamManagementService.htm)
* [DefaultUpstreamManagementService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Management_DefaultUpstreamManagementService.htm)

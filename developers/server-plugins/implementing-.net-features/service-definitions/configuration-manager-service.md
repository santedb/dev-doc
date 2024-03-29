`IConfigurationManager` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Contract for service implementations that manage the core SanteDB configuration

## Description
SanteDB plugins are expected to be portable and can run on a variety of platforms, in a variety of deployments, and a variety 
            of environments. This necessitates a consistent manner to manage configuration data for the SanteDB services. The [IConfigurationManager](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IConfigurationManager.htm)
            is responsible for this duty. Example implementations of this service may include:
            

* Loading configuration from a file stored on a local file system
* Loading configuration from a shared document-based database (for distributed configurations)
* Loading configuration from environment variables or synthesization classes (like in Docker)
* Loading/chaining configuration from another or central iCDR instance



            By default, the SanteDB iCDR and dCDR will use an XML or JSON file to store the configuration information, however the [SanteDBConfiguration](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Configuration_SanteDBConfiguration.htm)
            class can be shared on any number of transports.

# Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Configuration|SanteDBConfiguration|R|Get the entirety of the SanteDB configuration|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetSection|T|*none*|TODO|
|GetAppSetting|String|*String* **key**|Gets the specified application setting|
|GetConnectionString|ConnectionString|*String* **key**|Get the specified connection string to a database|
|SetAppSetting|void|*String* **key**<br/>*String* **value**|Set the specified application setting|
|Reload|void|*none*|TODO|

# Implementations


## DockerConfigurationManager - (SanteDB.Docker.Core)
TODO: Document this

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Docker.Core.DockerConfigurationManager, SanteDB.Docker.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Local File Configuration Manager - (SanteDB.Server.Core)
Provides a redirected configuration service which reads configuration information from a file
### Description
This configuration manager implementation  reads from the configuration file ```santedb.config.xml``` in the same directory
            as the installed iCDR instance. This file is create either manually ([as documented here](https://help.santesuite.org/operations/server-administration/host-configuration-file)), or
            using the [Configuration Tool](https://help.santesuite.org/operations/server-administration/configuration-tool).

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.FileConfigurationService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyConfigurationManager : SanteDB.Core.Services.IConfigurationManager { 
	public String ServiceName => "My own IConfigurationManager service";
	/// <summary>
	/// Get the entirety of the SanteDB configuration
	/// </summary>
	public SanteDBConfiguration Configuration {
		get;
	}
	public T GetSection<T>(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Gets the specified application setting
	/// </summary>
	public String GetAppSetting(String key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the specified connection string to a database
	/// </summary>
	public ConnectionString GetConnectionString(String key){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Set the specified application setting
	/// </summary>
	public void SetAppSetting(String key,String value){
		throw new System.NotImplementedException();
	}
	public void Reload(){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IConfigurationManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IConfigurationManager.htm)
* [DockerConfigurationManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Docker_Core_DockerConfigurationManager.htm)
* [FileConfigurationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_FileConfigurationService.htm)

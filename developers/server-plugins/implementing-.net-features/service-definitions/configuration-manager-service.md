`IConfigurationManager` in assembly SanteDB.Core.Api version 3.0.1980.0

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
|IsReadonly|Boolean|R|True if the configuration manager is readonly|
|Configuration|SanteDBConfiguration|R|Get the entirety of the SanteDB configuration|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetSection|T|*none*|TODO|
|GetAppSetting|String|*String* **key**|Gets the specified application setting|
|GetConnectionString|ConnectionString|*String* **key**|Get the specified connection string to a database|
|SetAppSetting|void|*String* **key**<br/>*String* **value**|Set the specified application setting|
|Reload|void|*none*|TODO|
|SaveConfiguration|void|*Boolean* **restart**|Save the configuration|
|SetTransientConnectionString|void|*String* **name**<br/>*ConnectionString* **connectionString**|Adds a connection string only for the lifetime of the server|

# Implementations


## InitialConfigurationManager - (SanteDB.Client)
A configuration manager which uses a temporary configuration in memory 
            via implementations of [IInitialConfigurationProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Configuration_IInitialConfigurationProvider.htm)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Configuration.InitialConfigurationManager, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Local File Configuration Manager - (SanteDB.Core.Api)
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
		<add type="SanteDB.Core.Services.Impl.FileConfigurationService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## DockerConfigurationManager - (SanteDB.Docker.Core)
A configuration manager which constructs a [SanteDBConfiguration](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Configuration_SanteDBConfiguration.htm) from environment variables
### Description
This implementation of the [IConfigurationManager](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IConfigurationManager.htm) uses environment variables passed from a 
            [Dockerized Installation Environment](https://help.santesuite.org/installation/installation/santedb-server/installation-using-appliances/docker-containers) so 
            that SanteDB modules may operate as though they were configured from a static configuration file. 

This class scans the ```SDB_FEATURE``` environment variables and locates the [IDockerFeature](http://santesuite.org/assets/doc/net/html/T_SanteDB_Docker_Core_IDockerFeature.htm) implementation 
            for the specified environment variable. It then calls the ```Configure()``` method on those implementations and builds
            an instance of the [SanteDBConfiguration](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Configuration_SanteDBConfiguration.htm) object based on those providers.

For more information about the Docker features and their configuration see the [Docker Feature documentation](https://help.santesuite.org/installation/installation/santedb-server/installation-using-appliances/docker-containers/feature-configuration) article

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Docker.Core.DockerConfigurationManager, SanteDB.Docker.Core, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
	/// True if the configuration manager is readonly
	/// </summary>
	public Boolean IsReadonly {
		get;
	}
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
	/// <summary>
	/// Save the configuration
	/// </summary>
	public void SaveConfiguration(Boolean restart){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Adds a connection string only for the lifetime of the server
	/// </summary>
	public void SetTransientConnectionString(String name,ConnectionString connectionString){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IConfigurationManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IConfigurationManager.htm)
* [InitialConfigurationManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Configuration_InitialConfigurationManager.htm)
* [FileConfigurationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_FileConfigurationService.htm)
* [DockerConfigurationManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Docker_Core_DockerConfigurationManager.htm)

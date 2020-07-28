---
description: IConfigurationManager (SanteDB.Core.Api)
---

## Summary
Represents a configuration manager service

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Configuration|SanteDBConfiguration|R|Get the configuration object|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetSection|T||TODO|
|GetAppSetting|String|*String* **key**|Gets the specified application setting|
|GetConnectionString|ConnectionString|*String* **key**|Get the specified connection string|
|SetAppSetting|void|*String* **key**<br/>*String* **value**|Set the specified application setting|
|Reload|void||TODO|

## Implementations


### ConfigurationContext - (SanteDB.Configuration)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Configuration.ConfigurationContext, SanteDB.Configuration, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

### Local Configuration Manager - (SanteDB.Core)
Provides a redirected configuration service which reads configuration from a different file

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.FileConfigurationService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

### TestConfigurationService - (SanteDB.Core.TestFramework)
TODO: Document this

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.TestFramework.TestConfigurationService, SanteDB.Core.TestFramework, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyConfigurationManager : SanteDB.Core.Services.IConfigurationManager { 
	public String ServiceName => "My own IConfigurationManager service";
	/// <summary>
	/// Get the configuration object
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
	/// Get the specified connection string
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

---
description: IRecordMatchingConfigurationService (SanteDB.Core.Api)
---

## Summary
Represents a service

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Configurations|System.Collections.Generic.IEnumerable&lt;System.String>|R|Gets the names of configurations in this provider|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetConfiguration|SanteDB.Core.Services.IRecordMatchingConfiguration|name <small style='border:solid 1px #aaa'>System.String</small>|Get the specified named configuration|
|SaveConfiguration|SanteDB.Core.Services.IRecordMatchingConfiguration|configuration <small style='border:solid 1px #aaa'>SanteDB.Core.Services.IRecordMatchingConfiguration</small>|Saves the specified configuration to the configuration service|

## Implementations


### FileMatchConfigurationProvider - (SanteDB.Matcher.Configuration.File)
Represents a configuration provider which is for matching

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Matcher.Configuration.File.FileMatchConfigurationProvider, SanteDB.Matcher.Configuration.File, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

### AppletMatchConfigurationProvider - (SanteDB.Matcher)
Applet match configuration provider loads match configurations from available applets

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Matcher.Services.AppletMatchConfigurationProvider, SanteDB.Matcher, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

### AssemblyMatchConfigurationProvider - (SanteDB.Matcher)
File based match configuration provider

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Matcher.Services.AssemblyMatchConfigurationProvider, SanteDB.Matcher, Version=2.0.27.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyRecordMatchingConfigurationService : SanteDB.Core.Services.IRecordMatchingConfigurationService { 
	public String ServiceName => "My own IRecordMatchingConfigurationService service";
	/// <summary>
	/// Gets the names of configurations in this provider
	/// </summary>
	public System.Collections.Generic.IEnumerable<System.String> Configurations {
		get;
	}
	/// <summary>
	/// Get the specified named configuration
	/// </summary>
	public SanteDB.Core.Services.IRecordMatchingConfiguration GetConfiguration(System.String name){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Saves the specified configuration to the configuration service
	/// </summary>
	public SanteDB.Core.Services.IRecordMatchingConfiguration SaveConfiguration(SanteDB.Core.Services.IRecordMatchingConfiguration configuration){
		throw new System.NotImplementedException();
	}
}
```

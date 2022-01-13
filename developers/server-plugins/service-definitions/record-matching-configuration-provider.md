Record Matching Configuration Provider (IRecordMatchingConfigurationService in SanteDB.Core.Api)

# Summary
Represents a service

# Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Configurations|IEnumerable&lt;IRecordMatchingConfiguration>|R|Gets the names of configurations in this provider|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetConfiguration|IRecordMatchingConfiguration|*String* **configurationId**|Get the specified named configuration|
|SaveConfiguration|IRecordMatchingConfiguration|*IRecordMatchingConfiguration* **configuration**|Saves the specified configuration to the configuration service|
|DeleteConfiguration|IRecordMatchingConfiguration|*String* **configurationId**|Delete the configuration|

# Implementations


## AppletMatchConfigurationProvider - (SanteDB.Matcher)
Applet match configuration provider loads match configurations from available applets

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Matcher.Services.AppletMatchConfigurationProvider, SanteDB.Matcher, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AssemblyMatchConfigurationProvider - (SanteDB.Matcher)
File based match configuration provider

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Matcher.Services.AssemblyMatchConfigurationProvider, SanteDB.Matcher, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## FileMatchConfigurationProvider - (SanteDB.Matcher)
Represents a configuration provider which is for matching

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Matcher.Services.FileMatchConfigurationProvider, SanteDB.Matcher, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MdmMatchConfigurationService - (SanteDB.Persistence.MDM)
A specialized match configuration service which wraps the already configured one

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.MDM.Services.MdmMatchConfigurationService, SanteDB.Persistence.MDM, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Matching;
/// Other usings here
public class MyRecordMatchingConfigurationService : SanteDB.Core.Matching.IRecordMatchingConfigurationService { 
	public String ServiceName => "My own IRecordMatchingConfigurationService service";
	/// <summary>
	/// Gets the names of configurations in this provider
	/// </summary>
	public IEnumerable<IRecordMatchingConfiguration> Configurations {
		get;
	}
	/// <summary>
	/// Get the specified named configuration
	/// </summary>
	public IRecordMatchingConfiguration GetConfiguration(String configurationId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Saves the specified configuration to the configuration service
	/// </summary>
	public IRecordMatchingConfiguration SaveConfiguration(IRecordMatchingConfiguration configuration){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Delete the configuration
	/// </summary>
	public IRecordMatchingConfiguration DeleteConfiguration(String configurationId){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IRecordMatchingConfigurationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Matching_IRecordMatchingConfigurationService.htm)
* [AppletMatchConfigurationProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Matcher_Services_AppletMatchConfigurationProvider.htm)
* [AssemblyMatchConfigurationProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Matcher_Services_AssemblyMatchConfigurationProvider.htm)
* [FileMatchConfigurationProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Matcher_Services_FileMatchConfigurationProvider.htm)
* [MdmMatchConfigurationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_MDM_Services_MdmMatchConfigurationService.htm)

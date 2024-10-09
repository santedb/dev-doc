`IDataQualityConfigurationProviderService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Data quality configuration provider service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetRuleSets|IEnumerable&lt;DataQualityRulesetConfiguration>|*Boolean* **includeObsolete**|Get data quality rule set|
|GetRuleSet|DataQualityRulesetConfiguration|*String* **id**|Get the rule set|
|RemoveRuleSet|void|*String* **id**|Delete rule set identified by|
|SaveRuleSet|DataQualityRulesetConfiguration|*DataQualityRulesetConfiguration* **configuration**|Save the specified ruleset|
|GetRulesForType|IEnumerable&lt;DataQualityResourceConfiguration>|*none*|TODO|
|GetRulesForType|IEnumerable&lt;DataQualityResourceConfiguration>|*Type* **forType**|Get rulesets for|

# Implementations


## FileSystemDataQualityConfigurationProvider - (SanteDB.Client.Disconnected)
File system data quality provider

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Disconnected.Services.FileSystemDataQualityConfigurationProvider, SanteDB.Client.Disconnected, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## LegacyRulesetConfigurationProvider - (SanteDB.Core.Api)
Get the ruleset list from configuration file

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Data.Quality.Configuration.LegacyRulesetConfigurationProvider, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AdoDataQualityConfigurationProvider - (SanteDB.Persistence.Data)
Represents an implementation of the [IDataQualityConfigurationProviderService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_IDataQualityConfigurationProviderService.htm) which stores data quality rules in the database.
### Description
This is useful for multi-application server environments where configurations are to be shared between instances

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.AdoDataQualityConfigurationProvider, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Data.Quality;
/// Other usings here
public class MyDataQualityConfigurationProviderService : SanteDB.Core.Data.Quality.IDataQualityConfigurationProviderService { 
	public String ServiceName => "My own IDataQualityConfigurationProviderService service";
	/// <summary>
	/// Get data quality rule set
	/// </summary>
	public IEnumerable<DataQualityRulesetConfiguration> GetRuleSets(Boolean includeObsolete){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the rule set
	/// </summary>
	public DataQualityRulesetConfiguration GetRuleSet(String id){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Delete rule set identified by
	/// </summary>
	public void RemoveRuleSet(String id){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Save the specified ruleset
	/// </summary>
	public DataQualityRulesetConfiguration SaveRuleSet(DataQualityRulesetConfiguration configuration){
		throw new System.NotImplementedException();
	}
	public IEnumerable<DataQualityResourceConfiguration> GetRulesForType<T>(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get rulesets for
	/// </summary>
	public IEnumerable<DataQualityResourceConfiguration> GetRulesForType(Type forType){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDataQualityConfigurationProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_IDataQualityConfigurationProviderService.htm)
* [FileSystemDataQualityConfigurationProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Disconnected_Services_FileSystemDataQualityConfigurationProvider.htm)
* [LegacyRulesetConfigurationProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_Configuration_LegacyRulesetConfigurationProvider.htm)
* [AdoDataQualityConfigurationProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoDataQualityConfigurationProvider.htm)

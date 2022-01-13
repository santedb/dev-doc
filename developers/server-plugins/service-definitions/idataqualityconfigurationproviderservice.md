---
description: IDataQualityConfigurationProviderService (IDataQualityConfigurationProviderService in SanteDB.Core.Api)
---

# Summary
Data quality configuration provider service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetRuleSets|IEnumerable&lt;DataQualityRulesetConfiguration>||TODO|
|GetRuleSet|DataQualityRulesetConfiguration|*String* **name**|Get the rule set|
|SaveRuleSet|DataQualityRulesetConfiguration|*DataQualityRulesetConfiguration* **configuration**|Save the specified ruleset|
|GetRulesForType|IEnumerable&lt;DataQualityResourceConfiguration>||TODO|

# Implementations


## LegacyRulesetConfigurationProvider - (SanteDB.Core.Api)
Get the ruleset list from configuration file

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Data.Quality.Configuration.LegacyRulesetConfigurationProvider, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
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
	public IEnumerable<DataQualityRulesetConfiguration> GetRuleSets(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the rule set
	/// </summary>
	public DataQualityRulesetConfiguration GetRuleSet(String name){
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
}
```

# References

* [IDataQualityConfigurationProviderService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_IDataQualityConfigurationProviderService.htm)
* [LegacyRulesetConfigurationProvider C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Quality_Configuration_LegacyRulesetConfigurationProvider.htm)

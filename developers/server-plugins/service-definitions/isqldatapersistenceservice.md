`ISqlDataPersistenceService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a data persistence service where arbitrary SQL can be run

# Properties

|Property|Type|Access|Description|
|-|-|-|-|
|InvariantName|String|R|Text that identifies the type of database system that is running|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|ExecuteNonQuery|void|*String* **sql**|Executes the arbitrary SQL|

# Implementations


## ADO.NET Data Persistence Service - (SanteDB.Persistence.Data.ADO)
Registers and configures the necessary sub-services and [IDataPersistenceService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataPersistenceService.htm) implementations
            to allow SanteDB iCDR to persist, query, and read messages from available ADO.NET data providers
### Description
This service is responsible for registering the necessary [IDataPersistenceService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataPersistenceService.htm) providers
            which are responsible for interfacing the SanteDB [Physical Model](https://help.santesuite.org/santedb/data-and-information-architecture/physical-model) 
            with the SanteDB [Business / Object Model](https://help.santesuite.org/santedb/data-and-information-architecture/conceptual-data-model). Each 
            persistence implementation is derived from the [ModelMap](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Map_ModelMap.htm) configuration, and is uses the ADO.NET classes to via the [IDbProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_OrmLite_Providers_IDbProvider.htm) configured.

Additionally, on start of the SanteDB iCDR or dCDR, this service is responsible for applying any [Data Patches](https://help.santesuite.org/developers/server-plugins/database-patching)
            which have been provided (compiled via an embedded resource) by any of the validated SanteDB plugins.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoPersistenceService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MySqlDataPersistenceService : SanteDB.Core.Services.ISqlDataPersistenceService { 
	public String ServiceName => "My own ISqlDataPersistenceService service";
	/// <summary>
	/// Text that identifies the type of database system that is running
	/// </summary>
	public String InvariantName {
		get;
	}
	/// <summary>
	/// Executes the arbitrary SQL
	/// </summary>
	public void ExecuteNonQuery(String sql){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ISqlDataPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ISqlDataPersistenceService.htm)
* [AdoPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoPersistenceService.htm)

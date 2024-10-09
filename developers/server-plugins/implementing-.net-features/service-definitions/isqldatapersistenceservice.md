`ISqlDataPersistenceService` in assembly SanteDB.Core.Api version 3.0.1980.0

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


## ADO.NET Persistence Service - (SanteDB.Persistence.Data)
A daemon service which registers the other persistence services

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.AdoPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
* [AdoPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoPersistenceService.htm)

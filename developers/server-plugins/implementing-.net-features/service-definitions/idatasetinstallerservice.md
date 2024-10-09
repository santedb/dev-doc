`IDatasetInstallerService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a service that can install [Dataset](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Initialization_Dataset.htm) files into the 
            registered [IDataPersistenceService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataPersistenceService.htm) instance

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Install|Boolean|*Dataset* **dataset**|Install the specified dataset|
|GetInstalled|IEnumerable&lt;String>|*none*|TODO|
|GetInstallDate|Nullable&lt;DateTimeOffset>|*String* **dataSetId**|Get the date that the specified dataset was installed|

# Implementations


## ADO.NET Dataset Installer - (SanteDB.Persistence.Data)
A [IDatasetInstallerService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Initialization_IDatasetInstallerService.htm) which can install datasets in ADO.NET persistence layer

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.AdoDatasetInstallerService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Data.Initialization;
/// Other usings here
public class MyDatasetInstallerService : SanteDB.Core.Data.Initialization.IDatasetInstallerService { 
	public String ServiceName => "My own IDatasetInstallerService service";
	/// <summary>
	/// Install the specified dataset
	/// </summary>
	public Boolean Install(Dataset dataset){
		throw new System.NotImplementedException();
	}
	public IEnumerable<String> GetInstalled(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the date that the specified dataset was installed
	/// </summary>
	public Nullable<DateTimeOffset> GetInstallDate(String dataSetId){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDatasetInstallerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Initialization_IDatasetInstallerService.htm)
* [AdoDatasetInstallerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoDatasetInstallerService.htm)

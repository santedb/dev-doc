`IForeignDataManagerService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a class which can manage the import and export of data to/from foreign data sources

## Description
In a data import, the SanteDB services use the following methodology:
            
1. The source data is first uploaded and stored in SanteDB in a staged form using this [IForeignDataManagerService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Import_IForeignDataManagerService.htm)
1. The source data is validated using the [IForeignDataFormat](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Import_IForeignDataFormat.htm) appropriate for its format, and rules in the [ForeignDataMap](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Import_Definition_ForeignDataMap.htm) selected
1. The source data is set as "ready for import" if the reviewer is satisfied with the outcome of the staging and validation
1. The staged data is then scheduled for processing on a background [IJob](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Jobs_IJob.htm) when the SanteDB instance is not busy and staged data is available
1. The staged data is processed and inserted into the underlying data persistence engine
1. Any rejected files are placed in a reject file

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Stage|IForeignDataSubmission|*Stream* **inputStream**<br/>*String* **name**<br/>*String* **description**<br/>*Guid* **foreignDataMapKey**<br/>*IDictionary&lt;String,String>* **parameterValues**|Stage the  for future processing|
|Schedule|IForeignDataSubmission|*Guid* **foreignDataId**|Updates the status of the foreign data information record to indicate it is ready for staging|
|Execute|IForeignDataSubmission|*Guid* **foreignDataId**|Execute the foreign data import info|
|Get|IForeignDataSubmission|*Guid* **foreignDataId**|Get the foreign data import information by UUID|
|Find|IQueryResultSet&lt;IForeignDataSubmission>|*Expression&lt;Func&lt;IForeignDataSubmission,Boolean>>* **query**|Find foreign data by identifier|
|Delete|IForeignDataSubmission|*Guid* **foreignDataId**|Delete foreign data from the server|

# Implementations


## UpstreamForeignDataManagement - (SanteDB.Client)
Upstream foreign data management classes

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Upstream.Management.UpstreamForeignDataManagement, SanteDB.Client, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AdoForeignDataManager - (SanteDB.Persistence.Data)
Foreign data manager which stores data about staged foreign data into the database

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.AdoForeignDataManager, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Data.Import;
/// Other usings here
public class MyForeignDataManagerService : SanteDB.Core.Data.Import.IForeignDataManagerService { 
	public String ServiceName => "My own IForeignDataManagerService service";
	/// <summary>
	/// Stage the  for future processing
	/// </summary>
	public IForeignDataSubmission Stage(Stream inputStream,String name,String description,Guid foreignDataMapKey,IDictionary<String,String> parameterValues){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Updates the status of the foreign data information record to indicate it is ready for staging
	/// </summary>
	public IForeignDataSubmission Schedule(Guid foreignDataId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Execute the foreign data import info
	/// </summary>
	public IForeignDataSubmission Execute(Guid foreignDataId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the foreign data import information by UUID
	/// </summary>
	public IForeignDataSubmission Get(Guid foreignDataId){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Find foreign data by identifier
	/// </summary>
	public IQueryResultSet<IForeignDataSubmission> Find(Expression<Func<IForeignDataSubmission,Boolean>> query){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Delete foreign data from the server
	/// </summary>
	public IForeignDataSubmission Delete(Guid foreignDataId){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IForeignDataManagerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Import_IForeignDataManagerService.htm)
* [UpstreamForeignDataManagement C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Upstream_Management_UpstreamForeignDataManagement.htm)
* [AdoForeignDataManager C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoForeignDataManager.htm)

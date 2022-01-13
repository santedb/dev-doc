Data Archiving Service (IDataArchiveService in SanteDB.Core.Api)

# Summary
Data Archive service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Archive|void|*Type* **modelType**<br/>*Guid[]* **keysToBeArchived**|Push the specified records to the archive|
|Retrieve|IdentifiedData|*Type* **modelType**<br/>*Guid* **keyToRetrieve**|Retrieve a record from the archive by key and type|
|Exists|Boolean|*Type* **modelType**<br/>*Guid* **keyToCheck**|Validates whether the specified key exists in the archive|
|Purge|void|*Type* **modelType**<br/>*Guid[]* **keysToBePurged**|Purge the specified object from the archive|

# Implementations


## ADO.NET Archiving and Data Shipping - (SanteDB.Persistence.Data.ADO)
The AdoArchiveService is an archival service which stores data in a secondary database

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoArchiveService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyDataArchiveService : SanteDB.Core.Services.IDataArchiveService { 
	public String ServiceName => "My own IDataArchiveService service";
	/// <summary>
	/// Push the specified records to the archive
	/// </summary>
	public void Archive(Type modelType,Guid[] keysToBeArchived){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Retrieve a record from the archive by key and type
	/// </summary>
	public IdentifiedData Retrieve(Type modelType,Guid keyToRetrieve){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Validates whether the specified key exists in the archive
	/// </summary>
	public Boolean Exists(Type modelType,Guid keyToCheck){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Purge the specified object from the archive
	/// </summary>
	public void Purge(Type modelType,Guid[] keysToBePurged){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDataArchiveService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataArchiveService.htm)
* [AdoArchiveService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoArchiveService.htm)

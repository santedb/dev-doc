`IDataArchiveService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Service contract for data archival and purging

## Description
The data archive service is used by various jobs throughout SanteDB iCDR (such as the [DataRetentionJob](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Jobs_DataRetentionJob.htm)) to 
            copy records which are past their retention rules to a secondary data storage facility. This service can be used for long-term
            archival of old (non-clinically relevant data) data and supports the purging of data which is no longer needed.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Archive|void|*Type* **modelType**<br/>*Guid[]* **keysToBeArchived**|Push the specified records to the archive|
|Retrieve|IdentifiedData|*Type* **modelType**<br/>*Guid* **keyToRetrieve**|Retrieve a record from the archive by key and type|
|Exists|Boolean|*Type* **modelType**<br/>*Guid* **keyToCheck**|Validates whether the specified key exists in the archive|
|Purge|void|*Type* **modelType**<br/>*Guid[]* **keysToBePurged**|Purge the specified object from the archive|

# Implementations

None

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

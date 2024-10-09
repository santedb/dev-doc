`ICdssLibraryRepository` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a generic repository which is used for the management of [ICdssAsset](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Cdss_ICdssAsset.htm)

## Description
The clinical protocol asset repository is responsible for the storage and creation of relevant 
            [ICdssProtocol](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Cdss_ICdssProtocol.htm) and [ICdssLibrary](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Cdss_ICdssLibrary.htm) instances which are used by the CDSS 
            engine to actually perform their duties

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Find|IQueryResultSet&lt;ICdssLibrary>|*Expression&lt;Func&lt;ICdssLibrary,Boolean>>* **filter**|Find all protocol assets which match the specified filter|
|Get|ICdssLibrary|*Guid* **libraryUuid**<br/>*Nullable&lt;Guid>* **versionUuid**|Get the protocol asset by identifier|
|InsertOrUpdate|ICdssLibrary|*ICdssLibrary* **libraryToInsert**|Insert a protocol asset into the store|
|Remove|ICdssLibrary|*Guid* **libraryUuid**|Remove a protocol asset from the repository by identifier|

# Implementations


## FileSystemCdssLibraryRepository - (SanteDB.Client.Disconnected)
A CDSS library repository that uses a file system for storage

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Client.Disconnected.Services.FileSystemCdssLibraryRepository, SanteDB.Client.Disconnected, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## AdoCdssLibraryRepository - (SanteDB.Persistence.Data)
Represents a CDSS library repository

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.AdoCdssLibraryRepository, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Cdss;
/// Other usings here
public class MyCdssLibraryRepository : SanteDB.Core.Cdss.ICdssLibraryRepository { 
	public String ServiceName => "My own ICdssLibraryRepository service";
	/// <summary>
	/// Find all protocol assets which match the specified filter
	/// </summary>
	public IQueryResultSet<ICdssLibrary> Find(Expression<Func<ICdssLibrary,Boolean>> filter){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get the protocol asset by identifier
	/// </summary>
	public ICdssLibrary Get(Guid libraryUuid,Nullable<Guid> versionUuid){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Insert a protocol asset into the store
	/// </summary>
	public ICdssLibrary InsertOrUpdate(ICdssLibrary libraryToInsert){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Remove a protocol asset from the repository by identifier
	/// </summary>
	public ICdssLibrary Remove(Guid libraryUuid){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ICdssLibraryRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Cdss_ICdssLibraryRepository.htm)
* [FileSystemCdssLibraryRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Client_Disconnected_Services_FileSystemCdssLibraryRepository.htm)
* [AdoCdssLibraryRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_AdoCdssLibraryRepository.htm)

`IDataManagementPattern` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Indicates a class is a data management pattern

## Description
This interface is a marker interface

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetLinkProvider|IDataManagedLinkProvider&lt;T>|*none*|TODO|
|GetLinkProvider|IDataManagedLinkProvider|*Type* **forType**|Get data management link provider for|

# Implementations


## SimDataManagementService - (SanteDB.Core.Api)
Represents a [IDataManagementPattern](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_IDataManagementPattern.htm) which uses destructive merge and matching in order
            to contain a single instance.
### Description
The SIM data management service implements the [Single Instance Mode](https://help.santesuite.org/santedb/data-storage-patterns#single-instance-mode) of
            storage pattern. The single instance mode:

* Maintains a single copy of a record in the CDR
* Attempts to perform duplicate detection between these single instances
* When a merge occurs, the subsumed record is obsoleted (and later purged)
* Unmerge is not possible

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Data.Management.SimDataManagementService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MDM Data Repository - (SanteDB.Persistence.MDM)
An implementation of the [IDataManagementPattern](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_IDataManagementPattern.htm) which keeps multiple copies of 
            source records and maintains linkages with a single master record.
### Description
The MDM data management service provides the [Master Data Storage](https://help.santesuite.org/santedb/data-storage-patterns/master-data-storage) pattern
            for SanteDB. This service is responsible for creating subscribers to listen to events from the [IRepositoryService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRepositoryService.htm) layer in SanteDB
            and take appropriate actions to seggregate source information form record of truth information. Additionally, this service registers implementations
            of [IFreetextSearchService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IFreetextSearchService.htm), [IRecordMatchingService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Matching_IRecordMatchingService.htm), [IRecordMergingService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRecordMergingService.htm) and [ISubscriptionExecutor](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ISubscriptionExecutor.htm) functionality to ensure the freetext and subscription requests are 
            properly handled and synthesized.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.MDM.Services.MdmDataManagementService, SanteDB.Persistence.MDM, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Data;
/// Other usings here
public class MyDataManagementPattern : SanteDB.Core.Data.IDataManagementPattern { 
	public String ServiceName => "My own IDataManagementPattern service";
	public IDataManagedLinkProvider<T> GetLinkProvider<T>(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get data management link provider for
	/// </summary>
	public IDataManagedLinkProvider GetLinkProvider(Type forType){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IDataManagementPattern C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_IDataManagementPattern.htm)
* [SimDataManagementService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Data_Management_SimDataManagementService.htm)
* [MdmDataManagementService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_MDM_Services_MdmDataManagementService.htm)

`IFreetextSearchService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Contract which defines free-text search functionality

## Description
In SanteDB HDSI, the ```_any``` parameter can be used by a client to indicate that the caller does not
            care which field the value matches, rather the client is performing a free-text or full-text search. Full text
            searches can be used to search for content like: ```John Smith HBA1C December```. Such requests are passed
            to the [IFreetextSearchService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IFreetextSearchService.htm) as a series of terms provided by the client.

Implementers are expected to call their full-text technology provider to perform the search. Additionally, 
            implementers should provide an [IJob](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Jobs_IJob.htm) implementation (or should subscribe to updates from the [IDataPersistenceService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IDataPersistenceService.htm))
            to maintain the index.

Implementations of the freetext search service may be technologies like Apache Lucene, PostgreSQL Free-Text Search, Amazon Elastic Search, etc.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Search|IEnumerable&lt;TEntity>|*String[]* **term**<br/>*Guid* **queryId**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**<br/>*ModelSort`1[]* **orderBy**|Search the provider of freetext indexing for any term provided|

# Implementations


## AdoFreetextSearchService - (SanteDB.Persistence.Data.ADO)
An implementation of the [IFreetextSearchService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IFreetextSearchService.htm) which uses the underlying built-in database functionality
### Description
This implementation of the free-text search service relies on a [IDbProvider](http://santesuite.org/assets/doc/net/html/T_SanteDB_OrmLite_Providers_IDbProvider.htm) implementation 
            providing a [IDbFilterFunction](http://santesuite.org/assets/doc/net/html/T_SanteDB_OrmLite_Providers_IDbFilterFunction.htm) with the identifier ```freetext```. The call is equivalent to using the 
            HDSI query expression: ```id=:(freetext|$term)``` and uses SanteDB's extended filter function (see an example
            of [implementing a custom IDbFilterFunction](https://help.santesuite.org/developers/server-plugins/custom-algorithms#implementing-custom-idbfilterfunction)

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.ADO.Services.AdoFreetextSearchService, SanteDB.Persistence.Data.ADO, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MdmFreetextSearchService - (SanteDB.Persistence.MDM)
Freetext search service that is Master Aware
### Description
Only use this freetext search service if your freetext search service implementation interacts directly with the
            SanteDB database, not if you're using something like Lucene or Redshift as those are index based and the fetch should
            be done via the IRepositoryService

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.MDM.Services.MdmFreetextSearchService, SanteDB.Persistence.MDM, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyFreetextSearchService : SanteDB.Core.Services.IFreetextSearchService { 
	public String ServiceName => "My own IFreetextSearchService service";
	/// <summary>
	/// Search the provider of freetext indexing for any term provided
	/// </summary>
	public IEnumerable<TEntity> Search<TEntity>(String[] term,Guid queryId,Int32 offset,Nullable<Int32> count,Int32& totalResults,ModelSort`1[] orderBy){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IFreetextSearchService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IFreetextSearchService.htm)
* [AdoFreetextSearchService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_ADO_Services_AdoFreetextSearchService.htm)
* [MdmFreetextSearchService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_MDM_Services_MdmFreetextSearchService.htm)

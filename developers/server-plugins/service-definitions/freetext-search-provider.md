`IFreetextSearchService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Free text search service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Search|IEnumerable&lt;TEntity>|*String[]* **term**<br/>*Guid* **queryId**<br/>*Int32* **offset**<br/>*Nullable&lt;Int32>* **count**<br/>*Int32&* **totalResults**<br/>*ModelSort`1[]* **orderBy**|Search based on tokens|

# Implementations


## AdoFreetextSearchService - (SanteDB.Persistence.Data.ADO)
Represents a basic ADO FreeText search service which really just filters on database tables

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
	/// Search based on tokens
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

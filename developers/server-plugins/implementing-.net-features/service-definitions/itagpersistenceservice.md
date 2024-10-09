`ITagPersistenceService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Taggable persistence service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Save|void|*Guid* **sourceKey**<br/>*ITag* **tag**|Save tag to source key|
|Save|void|*Guid* **sourceKey**<br/>*String* **tagName**<br/>*String* **tagValue**|Save tag to source key|

# Implementations


## Local Tag Persistence - (SanteDB.Core.Api)
Tag persistence service for tags - is used as a fallback as it is slower than using the ADO or remote tag service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.LocalTagPersistenceService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## TagPersistenceService - (SanteDB.Persistence.Data)
Tag persistence service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Persistence.Data.Services.Persistence.TagPersistenceService, SanteDB.Persistence.Data, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyTagPersistenceService : SanteDB.Core.Services.ITagPersistenceService { 
	public String ServiceName => "My own ITagPersistenceService service";
	/// <summary>
	/// Save tag to source key
	/// </summary>
	public void Save(Guid sourceKey,ITag tag){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Save tag to source key
	/// </summary>
	public void Save(Guid sourceKey,String tagName,String tagValue){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ITagPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ITagPersistenceService.htm)
* [LocalTagPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_LocalTagPersistenceService.htm)
* [TagPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Persistence_Data_Services_Persistence_TagPersistenceService.htm)

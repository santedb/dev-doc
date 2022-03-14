`ITagPersistenceService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Taggable persistence service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Save|void|*Guid* **sourceKey**<br/>*ITag* **tag**|Save tag to source key|

# Implementations


## Local Tag Persistence - (SanteDB.Server.Core)
Tag persistence service for act

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalTagPersistenceService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
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
}
```

# References

* [ITagPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ITagPersistenceService.htm)
* [LocalTagPersistenceService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalTagPersistenceService.htm)

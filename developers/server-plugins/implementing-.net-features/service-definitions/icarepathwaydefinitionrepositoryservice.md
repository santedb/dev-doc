`ICarePathwayDefinitionRepositoryService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
CAre pathway definition service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetCarepathDefinition|CarePathwayDefinition|*String* **mnemonic**|Get the specified care pathway which has the mnemonic|

# Implementations


## LocalCarePathwayDefinitionRepositoryService - (SanteDB.Core.Api)
Local care pathway definition

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalCarePathwayDefinitionRepositoryService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyCarePathwayDefinitionRepositoryService : SanteDB.Core.Services.ICarePathwayDefinitionRepositoryService { 
	public String ServiceName => "My own ICarePathwayDefinitionRepositoryService service";
	/// <summary>
	/// Get the specified care pathway which has the mnemonic
	/// </summary>
	public CarePathwayDefinition GetCarepathDefinition(String mnemonic){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ICarePathwayDefinitionRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ICarePathwayDefinitionRepositoryService.htm)
* [LocalCarePathwayDefinitionRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalCarePathwayDefinitionRepositoryService.htm)

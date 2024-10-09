`ITemplateDefinitionRepositoryService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a template definition repository which loads clinical template definitions

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetTemplateDefinition|TemplateDefinition|*String* **mnemonic**|Get tempate definition|

# Implementations


## LocalTemplateDefinitionRepositoryService - (SanteDB.Core.Api)
Represents a local metadata repository service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalTemplateDefinitionRepositoryService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyTemplateDefinitionRepositoryService : SanteDB.Core.Services.ITemplateDefinitionRepositoryService { 
	public String ServiceName => "My own ITemplateDefinitionRepositoryService service";
	/// <summary>
	/// Get tempate definition
	/// </summary>
	public TemplateDefinition GetTemplateDefinition(String mnemonic){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ITemplateDefinitionRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ITemplateDefinitionRepositoryService.htm)
* [LocalTemplateDefinitionRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalTemplateDefinitionRepositoryService.htm)

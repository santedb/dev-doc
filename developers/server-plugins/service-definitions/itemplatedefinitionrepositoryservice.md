`ITemplateDefinitionRepositoryService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a repository which deals with metadata such as assigning authorities,
            concept classes, etc.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GetTemplateDefinition|TemplateDefinition|*String* **mnemonic**|Get tempate definition|

# Implementations


## LocalTemplateDefinitionRepositoryService - (SanteDB.Server.Core)
Represents a local metadata repository service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalTemplateDefinitionRepositoryService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
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
* [LocalTemplateDefinitionRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalTemplateDefinitionRepositoryService.htm)

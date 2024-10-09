`IIdentityDomainRepositoryService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a repository service for managing assigning authorities.

## Description
This specialized [IRepositoryService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRepositoryService.htm) is intended to add functionality 
            to make the management of identity domains ([IdentityDomain](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_DataTypes_IdentityDomain.htm)) objects simpler by including 
            methods for getting domains by name and URI

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Get|IdentityDomain|*String* **domain**|Get by domain|
|Get|IdentityDomain|*Uri* **uri**|Get by domain|

# Implementations


## LocalIdentityDomainRepository - (SanteDB.Core.Api)
Represents a repository service for managing assigning authorities.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.Repository.LocalIdentityDomainRepository, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyIdentityDomainRepositoryService : SanteDB.Core.Services.IIdentityDomainRepositoryService { 
	public String ServiceName => "My own IIdentityDomainRepositoryService service";
	/// <summary>
	/// Get by domain
	/// </summary>
	public IdentityDomain Get(String domain){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get by domain
	/// </summary>
	public IdentityDomain Get(Uri uri){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IIdentityDomainRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IIdentityDomainRepositoryService.htm)
* [LocalIdentityDomainRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_Repository_LocalIdentityDomainRepository.htm)

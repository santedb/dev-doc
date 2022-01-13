Identity Domain Provider (IAssigningAuthorityRepositoryService in SanteDB.Core.Api)

# Summary
Represents a repository service for managing assigning authorities.

## Description
This specialized [IRepositoryService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRepositoryService.htm) is intended to add functionality 
            to make the management of identity domains ([AssigningAuthority](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_DataTypes_AssigningAuthority.htm)) objects simpler by including 
            methods for getting domains by name and URI

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Get|AssigningAuthority|*String* **domain**|Get by domain|
|Get|AssigningAuthority|*Uri* **uri**|Get by domain|

# Implementations


## LocalAssigningAuthorityRepository - (SanteDB.Server.Core)
Represents a repository service for managing assigning authorities.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalAssigningAuthorityRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyAssigningAuthorityRepositoryService : SanteDB.Core.Services.IAssigningAuthorityRepositoryService { 
	public String ServiceName => "My own IAssigningAuthorityRepositoryService service";
	/// <summary>
	/// Get by domain
	/// </summary>
	public AssigningAuthority Get(String domain){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Get by domain
	/// </summary>
	public AssigningAuthority Get(Uri uri){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IAssigningAuthorityRepositoryService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IAssigningAuthorityRepositoryService.htm)
* [LocalAssigningAuthorityRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalAssigningAuthorityRepository.htm)

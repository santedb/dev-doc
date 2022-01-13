`ICancelRepositoryService&lt;TModel>` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a repository that can cancel an act

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Cancel|TModel|*Guid* **id**|Cancels the specified object|

# Implementations


## GenericLocalActRepository&lt;TAct> - (SanteDB.Server.Core)
Represents an act repository service.

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.GenericLocalActRepository`1, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyCancelRepositoryService<TModel> : SanteDB.Core.Services.ICancelRepositoryService<TModel> { 
	public String ServiceName => "My own ICancelRepositoryService`1 service";
	/// <summary>
	/// Cancels the specified object
	/// </summary>
	public TModel Cancel(Guid id){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ICancelRepositoryService&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ICancelRepositoryService_1.htm)
* [GenericLocalActRepository&lt;TAct> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_GenericLocalActRepository_1.htm)

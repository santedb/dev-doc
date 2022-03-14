`ICancelRepositoryService&lt;TModel>` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a repository that can cancel an [Act](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_Act.htm) that is in progress

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Cancel|TModel|*Guid* **id**|Cancels the specified|

# Implementations


## GenericLocalActRepository&lt;TAct> - (SanteDB.Server.Core)
Represents an [IRepositoryService](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IRepositoryService.htm) which stores [Act](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Model_Acts_Act.htm)s and their derivative classes
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyCancelRepositoryService<TModel> : SanteDB.Core.Services.ICancelRepositoryService<TModel> { 
	public String ServiceName => "My own ICancelRepositoryService`1 service";
	/// <summary>
	/// Cancels the specified
	/// </summary>
	public TModel Cancel(Guid id){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ICancelRepositoryService&lt;TModel> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_ICancelRepositoryService_1.htm)
* [GenericLocalActRepository&lt;TAct> C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_GenericLocalActRepository_1.htm)

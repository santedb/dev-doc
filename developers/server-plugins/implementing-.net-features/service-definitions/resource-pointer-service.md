`IResourcePointerService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a service which is tasked with generating verified pointers to data

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GeneratePointer|String|*IHasIdentifiers* **entity**|Generate a structured pointer for the identified object|
|ResolveResource|IHasIdentifiers|*String* **pointerData**<br/>*Boolean* **validate**|Resolve the specified resource|

# Implementations


## JWS Resource Pointer - (SanteDB.Core.Api)
Represents a record pointer service using JWS

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Services.Impl.JwsResourcePointerService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyResourcePointerService : SanteDB.Core.Services.IResourcePointerService { 
	public String ServiceName => "My own IResourcePointerService service";
	/// <summary>
	/// Generate a structured pointer for the identified object
	/// </summary>
	public String GeneratePointer(IHasIdentifiers entity){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Resolve the specified resource
	/// </summary>
	public IHasIdentifiers ResolveResource(String pointerData,Boolean validate){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IResourcePointerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IResourcePointerService.htm)
* [JwsResourcePointerService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_JwsResourcePointerService.htm)

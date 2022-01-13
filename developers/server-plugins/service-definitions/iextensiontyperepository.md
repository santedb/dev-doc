`IExtensionTypeRepository` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents the extension type repository

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Get|ExtensionType|*Uri* **uri**|Get the xtension type my its url|

# Implementations


## LocalExtensionTypeRepository - (SanteDB.Server.Core)
Local extension types

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Services.Impl.LocalExtensionTypeRepository, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Services;
/// Other usings here
public class MyExtensionTypeRepository : SanteDB.Core.Services.IExtensionTypeRepository { 
	public String ServiceName => "My own IExtensionTypeRepository service";
	/// <summary>
	/// Get the xtension type my its url
	/// </summary>
	public ExtensionType Get(Uri uri){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IExtensionTypeRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_IExtensionTypeRepository.htm)
* [LocalExtensionTypeRepository C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Services_Impl_LocalExtensionTypeRepository.htm)

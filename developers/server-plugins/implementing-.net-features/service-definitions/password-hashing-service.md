`IPasswordHashingService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Password hashing service.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|ComputeHash|String|*String* **password**|Compute the password hash|
|ComputeHash|Byte[]|*Byte[]* **data**|Compute the password hash|

# Implementations


## SHA1 Password Encoding Service - (SanteDB.Core.Api)
SHA1 password generator service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.SHA1PasswordHashingService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SHA256 Password Encoding Service - (SanteDB.Core.Api)
SHA256 password generator service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.SHA256PasswordHashingService, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyPasswordHashingService : SanteDB.Core.Security.Services.IPasswordHashingService { 
	public String ServiceName => "My own IPasswordHashingService service";
	/// <summary>
	/// Compute the password hash
	/// </summary>
	public String ComputeHash(String password){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Compute the password hash
	/// </summary>
	public Byte[] ComputeHash(Byte[] data){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IPasswordHashingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IPasswordHashingService.htm)
* [SHA1PasswordHashingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_SHA1PasswordHashingService.htm)
* [SHA256PasswordHashingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_SHA256PasswordHashingService.htm)

Password Hashing Service (IPasswordHashingService in SanteDB.Core.Api)

# Summary
Password hashing service.

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|ComputeHash|String|*String* **password**|Compute the password hash|

# Implementations


## SHA1 Password Encoding Service - (SanteDB.Core.Api)
SHA1 password generator service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.SHA1PasswordHashingService, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
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
		<add type="SanteDB.Core.Security.SHA256PasswordHashingService, SanteDB.Core.Api, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SHA256 Password Encoding Service - (SanteDB.Server.Core)
SHA256 password generator service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Security.SHA256PasswordHashingService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## SHA1 Password Encoding Service - (SanteDB.Server.Core)
SHA1 password generator service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Security.SHA1PasswordHashingService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## MD5 Password Encoding Service - (SanteDB.Server.Core)
SHA1 password generator service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Security.MD5PasswordHashingService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

## Plaintext Password Encode - (SanteDB.Server.Core)
Plaintext password generator service

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Security.PlainPasswordHashingService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
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
}
```

# References

* [IPasswordHashingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IPasswordHashingService.htm)
* [SHA1PasswordHashingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_SHA1PasswordHashingService.htm)
* [SHA256PasswordHashingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_SHA256PasswordHashingService.htm)
* [SHA256PasswordHashingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Security_SHA256PasswordHashingService.htm)
* [SHA1PasswordHashingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Security_SHA1PasswordHashingService.htm)
* [MD5PasswordHashingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Security_MD5PasswordHashingService.htm)
* [PlainPasswordHashingService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Security_PlainPasswordHashingService.htm)

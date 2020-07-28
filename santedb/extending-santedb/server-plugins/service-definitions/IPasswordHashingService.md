---
description: IPasswordHashingService (SanteDB.Core.Api)
---

## Summary
Password hashing service.

## Implementations


### SHA256 Password Encoding Service - (SanteDB.Core)
SHA256 password generator service

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.SHA256PasswordHashingService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

### SHA1 Password Encoding Service - (SanteDB.Core)
SHA1 password generator service

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.SHA1PasswordHashingService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

### MD5 Password Encoding Service - (SanteDB.Core)
SHA1 password generator service

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.MD5PasswordHashingService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```

### Plaintext Password Encode - (SanteDB.Core)
Plaintext password generator service

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.PlainPasswordHashingService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyPasswordHashingService : SanteDB.Core.Security.Services.IPasswordHashingService { 
	public String ServiceName => "My own IPasswordHashingService service";
	/// <summary>
	/// Compute the password hash
	/// </summary>
	public System.String ComputeHash(System.String password){
		throw new System.NotImplementedException();
	}
}
```

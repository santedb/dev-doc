---
description: IPasswordValidatorService (SanteDB.Core.Api)
---

## Summary
Represents a password validation service

## Implementations


### Default Password Validator - (SanteDB.Core)
Represents a local regex password validator

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.DefaultPasswordValidationService, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyPasswordValidatorService : SanteDB.Core.Security.Services.IPasswordValidatorService { 
	public String ServiceName => "My own IPasswordValidatorService service";
	/// <summary>
	/// Validate the password
	/// </summary>
	public System.Boolean Validate(System.String password){
		throw new System.NotImplementedException();
	}
}
```

`IPasswordValidatorService` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Represents a password validation service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Validate|Boolean|*String* **password**|Validate the password|

# Implementations


## RegexPasswordValidator - (SanteDB.Core.Api)
Represents a regular expression password validator
{% hint style="info" %} This service implementation is abstract or is a generic definition. It is intended to be implemented or constructed at runtime from other services and cannot be used directly {% endhint %}

## Default Password Validator - (SanteDB.Server.Core)
Represents a local regex password validator

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Security.DefaultPasswordValidationService, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyPasswordValidatorService : SanteDB.Core.Security.Services.IPasswordValidatorService { 
	public String ServiceName => "My own IPasswordValidatorService service";
	/// <summary>
	/// Validate the password
	/// </summary>
	public Boolean Validate(String password){
		throw new System.NotImplementedException();
	}
}
```

# References

* [IPasswordValidatorService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_IPasswordValidatorService.htm)
* [RegexPasswordValidator C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Services_Impl_RegexPasswordValidator.htm)
* [DefaultPasswordValidationService C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Security_DefaultPasswordValidationService.htm)

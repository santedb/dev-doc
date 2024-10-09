`IPasswordValidatorService` in assembly SanteDB.Core.Api version 3.0.1980.0

# Summary
Represents a password validation service

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|Validate|Boolean|*String* **password**|Validate the password|

# Implementations


## RegexPasswordValidator - (SanteDB.Core.Api)
Represents a regular expression password validator

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.RegexPasswordValidator, SanteDB.Core.Api, Version=3.0.1980.0, Culture=neutral, PublicKeyToken=null" />
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
* [RegexPasswordValidator C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_RegexPasswordValidator.htm)

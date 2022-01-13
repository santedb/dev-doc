`ITwoFactorSecretGenerator` in assembly SanteDB.Core.Api version 2.1.151.0

# Summary
Identifies a class which can generate TFA secrets

# Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Name|String|R|Gets the name of the TFA generator|

# Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GenerateTfaSecret|String|*none*|TODO|
|Validate|Boolean|*String* **secret**|Validates the secret|

# Implementations


## Simple TFA Secret Generator - (SanteDB.Server.Core)
Represents a TFA secret generator which uses the server's clock

### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Server.Core.Security.SimpleTfaSecretGenerator, SanteDB.Server.Core, Version=2.1.151.0, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
# Example Implementation
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyTwoFactorSecretGenerator : SanteDB.Core.Security.Services.ITwoFactorSecretGenerator { 
	public String ServiceName => "My own ITwoFactorSecretGenerator service";
	/// <summary>
	/// Gets the name of the TFA generator
	/// </summary>
	public String Name {
		get;
	}
	public String GenerateTfaSecret(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Validates the secret
	/// </summary>
	public Boolean Validate(String secret){
		throw new System.NotImplementedException();
	}
}
```

# References

* [ITwoFactorSecretGenerator C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Core_Security_Services_ITwoFactorSecretGenerator.htm)
* [SimpleTfaSecretGenerator C# Documentation](http://santesuite.org/assets/doc/net/html/T_SanteDB_Server_Core_Security_SimpleTfaSecretGenerator.htm)

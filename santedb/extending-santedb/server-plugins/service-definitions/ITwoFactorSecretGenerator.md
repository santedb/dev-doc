---
description: ITwoFactorSecretGenerator (SanteDB.Core.Api)
---

## Summary
Identifies a class which can generate TFA secrets

## Implementations


### Simple TFA Secret Generator - (SanteDB.Core)
Represents a TFA secret generator which uses the server's clock

#### Service Registration
```markup
...
<section xsi:type="ApplicationServiceContextConfigurationSection" threadPoolSize="4">
	<serviceProviders>
		...
		<add type="SanteDB.Core.Security.SimpleTfaSecretGenerator, SanteDB.Core, Version=2.0.27.29201, Culture=neutral, PublicKeyToken=null" />
		...
	</serviceProviders>
```
## Example
```csharp
/// Example Implementation
using SanteDB.Core.Security.Services;
/// Other usings here
public class MyTwoFactorSecretGenerator : SanteDB.Core.Security.Services.ITwoFactorSecretGenerator { 
	public String ServiceName => "My own ITwoFactorSecretGenerator service";
	/// <summary>
	/// Gets the name of the TFA generator
	/// </summary>
	public System.String Name {
		get;
	}
	public System.String GenerateTfaSecret(){
		throw new System.NotImplementedException();
	}
	/// <summary>
	/// Validates the secret
	/// </summary>
	public System.Boolean Validate(System.String secret){
		throw new System.NotImplementedException();
	}
}
```

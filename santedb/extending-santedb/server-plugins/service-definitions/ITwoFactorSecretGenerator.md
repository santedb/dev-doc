---
description: ITwoFactorSecretGenerator (SanteDB.Core.Api)
---

## Summary
Identifies a class which can generate TFA secrets

## Events

|Event|Type|Description|
|-|-|-|

## Properties

|Property|Type|Access|Description|
|-|-|-|-|
|Name|String|R|Gets the name of the TFA generator|

## Operations

|Operation|Response/Return|Input/Parameter|Description|
|-|-|-|-|
|GenerateTfaSecret|String||TODO|
|Validate|Boolean|secret <small style='border:solid 1px #aaa'>String</small>|Validates the secret|

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
